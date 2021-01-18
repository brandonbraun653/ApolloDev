cmake_minimum_required(VERSION 3.18.0)
project(ApolloDev VERSION 1.0 LANGUAGES C CXX ASM)


set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)


# ====================================================
# Perform very high level configuration
# ====================================================
include("lib/CommonTools/cmake/options/common.cmake")
add_subdirectory("${COMMON_TOOL_ROOT}/cmake/device/am335x" ${PROJECT_BINARY_DIR}/DeviceTarget)



add_subdirectory(test/bringup/jtag_loader)
