cmake_minimum_required(VERSION 3.6)

add_library(inventory STATIC src/weapon.cpp include/inventory/weapon.h)

target_include_directories(inventory PUBLIC include PRIVATE include/inventory)

include_directories(include)