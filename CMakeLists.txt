cmake_minimum_required(VERSION 3.10)

list(INSERT CMAKE_MODULE_PATH 0 "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

project(tbsgNetLib VERSION 0.0.1 DESCRIPTION "A great new project")

include(GitSubmodule)
include(target_source_local)
GitSubmodule()
# Include third-party components we need for the build
add_subdirectory(third_party)

add_subdirectory(src)

