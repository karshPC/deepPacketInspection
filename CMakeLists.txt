cmake_minimum_required(VERSION 3.16)
project(PacketAnalyzer VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Header files location
include_directories(${CMAKE_SOURCE_DIR}/include)

# ---- Target 1: packet_analyzer (simple packet dumper) ----
set(ANALYZER_SOURCES
    src/main.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
)
add_executable(packet_analyzer ${ANALYZER_SOURCES})

# ---- Target 2: dpi_engine (multi-threaded DPI + blocking engine) ----
set(DPI_SOURCES
    src/dpi_mt.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
    src/sni_extractor.cpp
    src/types.cpp
)
add_executable(dpi_engine ${DPI_SOURCES})

find_package(Threads REQUIRED)
target_link_libraries(dpi_engine PRIVATE Threads::Threads)

# For macOS, we might need to link against system libraries later
if(APPLE)
    # Add any macOS-specific settings here
endif()