add_library(
    tbsgNetLib
    tbsg/tbsgNetLib.hpp
    tbsg/tbsgNetLib.cpp
    )
add_library(tbsg::tbsgNetLib ALIAS tbsgNetLib)
target_include_directories(tbsgNetLib
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
    PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    )
