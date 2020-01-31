cmake_minimum_required(VERSION 3.10)
project(ptl VERSION 0.0.1 DESCRIPTION "A great new project")

add_library(ptl STATIC
src/memory/Allocator.cpp
src/memory/default_memresource.cpp
src/memory/freelist_resources_win.cpp
src/memory/malloc_resource.cpp
src/memory/monotonic_resource_win.cpp
src/memory/new.cpp
src/memory/pool_resource.cpp
src/memory/RapidJsonAllocator.cpp
src/memory/String.cpp
)




target_include_directories(ptl
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
    PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    )

target_compile_features(ptl PUBLIC cxx_std_14)