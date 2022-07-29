add_library(
    Pcap++
    src/DpdkDevice.cpp
    src/DpdkDeviceList.cpp
    src/KniDevice.cpp
    src/KniDeviceList.cpp
    src/LinuxNicInformationSocket.cpp
    src/MBufRawPacket.cpp
    src/LinuxNicInformationSocket.cpp
    src/NetworkUtils.cpp
    src/PcapDevice.cpp
    src/PcapFileDevice.cpp
    src/PcapFilter.cpp
    src/PcapLiveDevice.cpp
    src/PcapLiveDeviceList.cpp
    src/PcapRemoteDevice.cpp
    src/PcapRemoteDeviceList.cpp
    src/PfRingDevice.cpp
    src/PfRingDeviceList.cpp
    src/RawSocketDevice.cpp
    src/WinPcapLiveDevice.cpp
    # Force light pcapng to be link fully static
    $<TARGET_OBJECTS:light_pcapng>
)

set(
    public_headers
    header/Device.h
    header/DpdkDevice.h
    header/DpdkDeviceList.h
    header/KniDevice.h
    header/KniDeviceList.h
    header/LinuxNicInformationSocket.h
    header/MBufRawPacket.h
    header/NetworkUtils.h
    header/PcapDevice.h
    header/PcapFileDevice.h
    header/PcapFilter.h
    header/PcapLiveDevice.h
    header/PcapLiveDeviceList.h
    header/PcapRemoteDevice.h
    header/PcapRemoteDeviceList.h
    header/PfRingDevice.h
    header/PfRingDeviceList.h
    header/RawSocketDevice.h
    header/WinPcapLiveDevice.h
)

set_property(TARGET Pcap++ PROPERTY PUBLIC_HEADER ${public_headers})

target_include_directories(
    Pcap++
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/header>
        $<INSTALL_INTERFACE:include/pcapplusplus>
    # Don't link with EndianPortable nor Light_PcapNG as they won't be exported
    PRIVATE $<TARGET_PROPERTY:EndianPortable,INTERFACE_INCLUDE_DIRECTORIES>
    $<TARGET_PROPERTY:light_pcapng,INTERFACE_INCLUDE_DIRECTORIES>
)

target_link_libraries(Pcap++ PUBLIC Common++ Packet++ PCAP::PCAP Threads::Threads)

install(
    TARGETS Pcap++
    EXPORT PcapPlusPlusTargets
    ARCHIVE DESTINATION ${PCAPP_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${PCAPP_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${PCAPP_INSTALL_INCLUDEDIR}
)

set_property(TARGET Pcap++ PROPERTY OUTPUT_NAME "pcap++")
set_property(TARGET Pcap++ PROPERTY VERSION ${PCAPP_VERSION})
