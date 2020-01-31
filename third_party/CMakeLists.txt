add_subdirectory(enet)
add_library(enet::enet STATIC IMPORTED)
set_target_properties(enet::enet PROPERTIES
    INCLUDE_DIRECTORIES ${PROJECT_SOURCE_DIR}/third_party/enet/include/
)
add_subdirectory(openssl-cmake)
add_subdirectory(ptl)
add_subdirectory(basiclogger)
add_library(FlatValueMap INTERFACE)
target_include_directories(FlatValueMap INTERFACE "FlatValueMap/include/")

