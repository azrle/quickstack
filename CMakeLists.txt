project(quickstack)
cmake_minimum_required(VERSION 2.8)
include(CPack)

# set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-std=gnu++0x")
set(SOURCE quickstack.cc)
# set(BINUTILS_LIB_DIR /opt/rh/devtoolset-2/root/usr/lib64 /usr/binutils/lib /usr/binutils/lib64)
set(BINUTILS_LIB_DIR /opt/rh/devtoolset-2/root/usr/lib64)
set(CMAKE_C_COMPILER   "/opt/rh/devtoolset-2/root/usr/bin/gcc")
set(CMAKE_CXX_COMPILER "/opt/rh/devtoolset-2/root/usr/bin/g++")

find_library(BINUTILS_LIB NAMES bfd
  PATHS ${BINUTILS_LIB_DIR}
  NO_DEFAULT_PATH)
find_library(BINUTILS_ELF_LIB NAMES elf
  PATHS ${BINUTILS_LIB_DIR}
  NO_DEFAULT_PATH)
find_library(BINUTILS_IBERTY_LIB NAMES iberty
  PATHS ${BINUTILS_LIB_DIR}
  NO_DEFAULT_PATH)

find_path(BINUTILS_INCLUDE_DIR  bfd.h
  /usr/binutils/include)
include_directories(${BINUTILS_INCLUDE_DIR})

add_executable(quickstack ${SOURCE})
target_link_libraries(quickstack
  z ${BINUTILS_LIB} ${BINUTILS_ELF_LIB} ${BINUTILS_IBERTY_LIB})

install(TARGETS quickstack DESTINATION bin)

