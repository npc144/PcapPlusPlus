add_executable(
    Pcap++Test
    main.cpp
    Common/TestUtils.cpp
    Tests/DpdkTests.cpp
    Tests/FileTests.cpp
    Tests/FilterTests.cpp
    Tests/IPFragmentationTests.cpp
    Tests/IpMacTests.cpp
    Tests/KniTests.cpp
    Tests/LiveDeviceTests.cpp
    Tests/LoggerTests.cpp
    Tests/PacketParsingTests.cpp
    Tests/PfRingTests.cpp
    Tests/RawSocketTests.cpp
    Tests/TcpReassemblyTests.cpp
)

target_link_libraries(
    Pcap++Test
    PUBLIC memplumber Pcap++ PcppTestFramework EndianPortable
)

add_test(
    NAME Pcap++Test
    COMMAND $<TARGET_FILE:Pcap++Test> -n
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
)