cmake_minimum_required(VERSION 2.80)
project (crow_sample0)

#if(EXISTS "${CMAKE_BINARY_DIR}/conanbuildinfo.cmake")
#    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
#    conan_basic_setup()
#endif()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
set(OPENSSL_ROOT_DIR "/usr/local/Cellar/openssl/1.0.2o_2")

find_package(Tcmalloc)
find_package(Threads)
find_package(OpenSSL)

if(OPENSSL_FOUND)
    include_directories(${OPENSSL_INCLUDE_DIR})
endif()

find_program(CCACHE_FOUND ccache)
#if(CCACHE_FOUND)
#    message("Found ccache ${CCACHE_FOUND}")
#    message("Using ccache to speed up compilation")
#    set(ENV{CCACHE_CPP2} "yes")
#    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache)
#    set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache)
#endif(CCACHE_FOUND)
#
#if (NOT CMAKE_BUILD_TYPE)
#    message(STATUS "No build type selected, default to Release")
#    set(CMAKE_BUILD_TYPE "Release")
#endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++1y -pedantic -Wextra")
find_package( Boost 1.52 COMPONENTS system thread REQUIRED )

include_directories( ${Boost_INCLUDE_DIR} )

set(PROJECT_INCLUDE_DIR
        ${PROJECT_SOURCE_DIR}/include)

include_directories("${PROJECT_INCLUDE_DIR}")
include_directories("${PROJECT_SOURCE_DIR}")
include_directories($ENV{HOME}/workSpace/oss/crow/include)

add_executable(crow_sample0 main.cpp)
target_link_libraries(crow_sample0 ${Boost_LIBRARIES})