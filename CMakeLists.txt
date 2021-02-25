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

# Override the linker command
# if(Toolchain::HAS_GCC_ARM_NONE_EABI OR Toolchain::HAS_GCC)
#   include("lib/CommonTools/cmake/toolchains/linker_whole_archive.cmake")
# endif()

# Select a global target flag
if(Toolchain::HAS_GCC_ARM_NONE_EABI)
  add_compile_definitions(EMBEDDED)
elseif(Toolchain::HAS_GCC)
  add_compile_definitions(SIMULATOR)
endif()

# ====================================================
# Import common packages and projects
# ====================================================
find_package(Boost REQUIRED)
add_subdirectory("lib/Aurora")
add_subdirectory("lib/Chimera")
add_subdirectory("lib/ChimeraSim")
add_subdirectory("lib/CommonTools/googletest")

add_subdirectory(Apollo)
add_subdirectory(test/bringup/jtag_loader)
