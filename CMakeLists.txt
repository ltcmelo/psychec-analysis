cmake_minimum_required(VERSION 2.8)

project(psychec-analysis)

set(CMAKE_MACOSX_RPATH TRUE)
set(CMAKE_INSTALL_RPATH "\$ORIGIN;@executable_path;@loader_path")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(PSYCHEC_CXX_FLAGS)
set(PSYCHEC_CXX_FLAGS "${PSYCHEC_CXX_FLAGS} -Wall")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_GLIBCXX_USE_CXX11_ABI=1")
add_definitions(-D_GLIBCXX_USE_CXX11_ABI=1)

set(SOURCES
    ${PROJECT_SOURCE_DIR}/Analysis.cpp
)

foreach(file ${SOURCES})
    set_source_files_properties(
        ${file} PROPERTIES
        COMPILE_FLAGS "${PSYCHEC_CXX_FLAGS}"
    )
endforeach()

include_directories(
    /Users/leandromelo/projects/Psyche-C/scm/psychec/C
)

add_library(psychec-analysis SHARED ${SOURCES})

target_link_libraries(psychec-analysis
    PRIVATE
    /Users/leandromelo/projects/Psyche-C/scm/psychec/C/libpsychecfe.dylib
)
