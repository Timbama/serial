cmake_minimum_required(VERSION 3.0)
add_library(serial SHARED)
find_package(Threads REQUIRED)
find_library(LIBRT rt)
target_sources(serial
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/serial.cc
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/impl/unix.cc
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/impl/list_ports/list_ports_linux.cc
)
target_include_directories(serial
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include
)
target_link_libraries(serial
    PRIVATE rt 
    PRIVATE pthread
)
## Install executable
set_target_properties(serial
    PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
)

