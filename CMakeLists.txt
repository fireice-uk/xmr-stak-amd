project(xmr-stak-amd)

cmake_minimum_required(VERSION 3.1.3)

# enforce C++11
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 11)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}" CACHE PATH "install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

# help to find AMD app SDK on systems with a software module system
list(APPEND CMAKE_PREFIX_PATH "$ENV{AMDAPPSDKROOT}")
# allow user to extent CMAKE_PREFIX_PATH via environment variable
list(APPEND CMAKE_PREFIX_PATH "$ENV{CMAKE_PREFIX_PATH}")

################################################################################
# CMake user options
################################################################################

# gcc 5.1 is the first GNU version without CoW strings
# https://github.com/fireice-uk/xmr-stak-nvidia/pull/10#issuecomment-290821792
# If you remove this guard to compile with older gcc versions the miner will produce
# a high rate of wrong shares.
if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    if(CMAKE_CXX_COMPILER_VERSION VERSION_LESS 5.1)
        message(FATAL_ERROR "GCC version must be at least 5.1!")
    endif()
endif()

set(BUILD_TYPE "Release;Debug")
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build" FORCE)
endif()
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "${BUILD_TYPE}")

# option to add static libgcc and libstdc++
option(CMAKE_LINK_STATIC "link as much as possible libraries static" OFF)

###############################################################################
# Find OpenCL
###############################################################################

find_package(OpenCL REQUIRED)
include_directories(SYSTEM ${OpenCL_INCLUDE_DIRS})
set(LIBS ${LIBS} ${OpenCL_LIBRARY})
link_directories(${OpenCL_LIBRARY})

################################################################################
# Find PThreads
################################################################################

find_package(Threads REQUIRED)
set(LIBS ${LIBS} ${CMAKE_THREAD_LIBS_INIT})

################################################################################
# Find microhttpd
################################################################################

option(MICROHTTPD_ENABLE "Enable or disable the requirement of microhttp (http deamon)" ON)
if(MICROHTTPD_ENABLE)
    find_library(MHTD NAMES microhttpd)
    if("${MHTD}" STREQUAL "MHTD-NOTFOUND")
        message(FATAL_ERROR "microhttpd NOT found: use `-DMICROHTTPD_ENABLE=OFF` to build without http deamon support")
    else()
        set(LIBS ${LIBS} ${MHTD})
    endif()
else()
    add_definitions("-DCONF_NO_HTTPD")
endif()

###############################################################################
# Find OpenSSL
###############################################################################

option(OpenSSL_ENABLE "Enable or disable the requirement of OpenSSL" ON)
if(OpenSSL_ENABLE)
    find_package(OpenSSL)
    if(OPENSSL_FOUND)
        include_directories(${OPENSSL_INCLUDE_DIR})
        set(LIBS ${LIBS} ${OPENSSL_LIBRARIES})
    else()
        message(FATAL_ERROR "OpenSSL NOT found: use `-DOpenSSL_ENABLE=OFF` to build without SSL support")
    endif()
else()
    add_definitions("-DCONF_NO_TLS")
endif()

################################################################################
# Compile & Link
################################################################################

include_directories(.)

# activate sse2 and aes-ni
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -msse2 -maes")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -msse2 -maes")

# activate static libgcc and libstdc++ linking
if(CMAKE_LINK_STATIC)
    set(BUILD_SHARED_LIBRARIES OFF)
    set(DL_LIB ${CMAKE_DL_LIBS})
    set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
    set(LIBS "-static-libgcc -static-libstdc++ ${LIBS}")
endif()

file(GLOB SRCFILES_CPP "*.cpp" "crypto/*.cpp")
file(GLOB SRCFILES_C "crypto/*.c" "amd_gpu/*.c")

add_library(xmr-stak-amd-c
    STATIC
    ${SRCFILES_C}
)
set_property(TARGET xmr-stak-amd-c PROPERTY C_STANDARD 99)
target_link_libraries(xmr-stak-amd-c PUBLIC ${OpenCL_LIBRARY})

add_executable(xmr-stak-amd
    ${SRCFILES_CPP}
)
set(EXECUTABLE_OUTPUT_PATH "bin")
target_link_libraries(xmr-stak-amd ${LIBS} xmr-stak-amd-c)

################################################################################
# Install
################################################################################

# do not install the binary if the project and install are equal
if( NOT "${CMAKE_INSTALL_PREFIX}" STREQUAL "${PROJECT_BINARY_DIR}" )
    install(TARGETS xmr-stak-amd
            RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")
endif()

install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/opencl"
        DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")

# avoid overwrite of user defined settings
# install `config.txt`if file not exists in `${CMAKE_INSTALL_PREFIX}/bin`
install(CODE " \
    if(NOT EXISTS ${CMAKE_INSTALL_PREFIX}/bin/config.txt)\n   \
        file(INSTALL ${CMAKE_CURRENT_SOURCE_DIR}/config.txt   \
            DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)\n        \
    endif()"
)
