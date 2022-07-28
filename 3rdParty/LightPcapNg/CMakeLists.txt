cmake_minimum_required(VERSION 3.12)

project(light_pcapng C)

add_library(
    light_pcapng OBJECT
    LightPcapNg/src/light_advanced.c
    LightPcapNg/src/light_alloc.c
    LightPcapNg/src/light_compression.c
    LightPcapNg/src/light_internal.c
    LightPcapNg/src/light_io.c
    LightPcapNg/src/light_manipulate.c
    LightPcapNg/src/light_null_compression.c
    LightPcapNg/src/light_option.c
    LightPcapNg/src/light_pcapng_cont.c
    LightPcapNg/src/light_pcapng_ext.c
    LightPcapNg/src/light_pcapng.c
    LightPcapNg/src/light_platform.c
    LightPcapNg/src/light_zstd_compression.c
)

target_compile_definitions(light_pcapng PUBLIC -DUNIVERSAL)

if(BUILD_SHARED_LIBS)
    set_property(TARGET light_pcapng PROPERTY POSITION_INDEPENDENT_CODE ON)
endif()

target_include_directories(
    light_pcapng
    PUBLIC $<INSTALL_INTERFACE:include>
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/LightPcapNg/include>
)
