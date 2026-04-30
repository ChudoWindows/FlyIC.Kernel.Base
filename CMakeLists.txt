cmake_minimum_required(VERSION 3.20)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib/${CMAKE_BUILD_TYPE})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib/${CMAKE_BUILD_TYPE})

set(ProjectName FlyIC.Kernel.Base)
project(${ProjectName})

set(COMPILE_BASE_FLAGS -nostdlib -ffreestanding -noinc++ -fno-exceptions -fno-rtti -fno-stack-protector)
set(LINK_BASE_FLAGS -nostdlib -Wl,e,startup -fuse-ld=lld)

if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
	set(COMPILE_EXT_FLAGS -g -O0)
else()
	set(COMPILE_EXT_FLAGS -g0 -O2)
endif()

include_directories(${CMAKE_SOURCE_DIR}/include)

add_library(${ProjectName} STATIC src/lib.cpp)

set_target_properties(${ProjectName} PROPERTIES PREFIX "")

target_compile_options(${ProjectName} PRIVATE ${COMPILE_BASE_FLAGS} ${COMPILE_EXT_FLAGS})
target_link_options(${ProjectName} PRIVATE ${LINK_BASE_FLAGS})
