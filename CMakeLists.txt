cmake_minimum_required (VERSION 3.1...3.27)
project(IcebergHashTable)

add_compile_options(-march=native)
include_directories(include)

add_library(ice_pc src/partitioned_counter.c src/lock.c)
add_library(ice_hashutil src/hashutil.c)
target_link_libraries(ice_hashutil ssl crypto)

add_library(iceberg src/iceberg_table.c)
target_link_libraries(iceberg ssl crypto ice_pc ice_hashutil)
target_include_directories(iceberg PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)