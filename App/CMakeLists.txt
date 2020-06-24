
cmake_minimum_required(VERSION 3.6)


# ----------------------------------------------- Variables -------------------------------------------

set(CMAKE_MODULE_PATH "D:/work/CMake/" ${CMAKE_MODULE_PATH})
set(CMAKE_DISABLE_PRECOMPILE_HEADERS ON CACHE BOOL "")

set(default_build_type "Release")
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to '${default_build_type}' as none was specified.")
  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE
      STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS
    "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()

include(${CMAKE_MODULE_PATH}/Helpers.cmake)

print("${PROJECT_SOURCE_DIR}")

# ----------------------------------------------- Target ----------------------------------------------

project(MyProject VERSION 1.0
                  DESCRIPTION "Very nice project"
                  LANGUAGES CXX)

add_executable(myExe src/main.cpp src/monster.cpp src/character.cpp include/character.h include/monster.h)

target_include_directories(myExe PUBLIC include)

# --------------------------------------------- Dependencies --------------------------------------------

add_subdirectory(../Inventory ${CMAKE_BINARY_DIR}/inventory)
add_subdirectory(../PrecompileHeader ${CMAKE_BINARY_DIR}/pheader)

target_link_libraries(myExe inventory)
target_link_libraries(myExe pheader)

target_precompile_headers(myExe REUSE_FROM pheader)

# ------------------------------------------- Compile Options -----------------------------------------

target_compile_features(myExe PUBLIC cxx_std_11)
set_target_properties(myExe PROPERTIES LINKER_LANGUAGE CXX)

#set_target_properties(myExe PROPERTIES INTERPROCEDURAL_OPTIMIZATION TRUE)