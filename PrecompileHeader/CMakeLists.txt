cmake_minimum_required(VERSION 3.6)

add_library(pheader STATIC pcheader.cpp pcheader.h)

target_include_directories(pheader PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_precompile_headers(pheader PUBLIC pcheader.h)


#--------------------------------------------- Dependencies -----------------------------------------------------

target_link_libraries(pheader inventory)

#--------------------------------------------- Compile Options -----------------------------------------------------

set_target_properties(pheader PROPERTIES LINKER_LANGUAGE CXX)
target_compile_features(pheader PUBLIC cxx_std_11)