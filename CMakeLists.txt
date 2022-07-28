cmake_minimum_required(VERSION 3.12)

# MAIN_PROJECT CHECK
set(MAIN_PROJECT OFF)
if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    set(MAIN_PROJECT ON)
endif()

set(PCAPP_VERSION 22.05)

project(
    PcapPlusPlus
    DESCRIPTION
    "PcapPlusPlus is a multi-platform C++ library for capturing, parsing and crafting of network packets."
    VERSION ${PCAPP_VERSION}
)
set(CMAKE_PROJECT_HOMEPAGE_URL "https://pcapplusplus.github.io/")

# Install dirs
if (NOT CMAKE_INSTALL_LIBDIR)
    set(CMAKE_INSTALL_LIBDIR lib)
endif()
if (NOT CMAKE_INSTALL_BINDIR)
    set(CMAKE_INSTALL_BINDIR bin)
endif()
if (NOT CMAKE_INSTALL_INCLUDEDIR)
    set(CMAKE_INSTALL_INCLUDEDIR include)
endif()
set(PCAPP_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR}/pcapplusplus)
set(PCAPP_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR}/pcapplusplus)
set(PCAPP_INSTALL_CMAKEDIR ${CMAKE_INSTALL_LIBDIR}/cmake/pcapplusplus)

# Set C++11
set(CMAKE_CXX_STANDARD 11)
# popen()/pclose() are not C++ standards
set(CMAKE_CXX_EXTENSIONS ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE
            "Release"
            CACHE STRING "Choose the type of build." FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release")
endif()

if(TARGET_COMPILER_CLANG OR TARGET_COMPILER_GCC)
    add_compile_options(-Wall)
endif()

enable_testing()

add_subdirectory(3rdParty)
add_subdirectory(Common++)
add_subdirectory(Packet++)
add_subdirectory(Pcap++)
add_subdirectory(Tests)
