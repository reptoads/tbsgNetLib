project(BasicLogger CXX)

################################################################################
# Source groups
################################################################################
set(Headers
    "external/fmt/include/fmt/chrono.h"
    "external/fmt/include/fmt/color.h"
    "external/fmt/include/fmt/core.h"
    "external/fmt/include/fmt/format-inl.h"
    "external/fmt/include/fmt/format.h"
    "external/fmt/include/fmt/locale.h"
    "external/fmt/include/fmt/ostream.h"
    "external/fmt/include/fmt/posix.h"
    "external/fmt/include/fmt/printf.h"
    "external/fmt/include/fmt/ranges.h"
    "external/fmt/include/fmt/time.h"
    "include/BasicLogger.h"
    "include/Details/GlobalLoggerInstance.h"
    "include/Logger.h"
    "include/LoggingFunction.h"
    "include/LoggingMacros.h"
    "include/Sinks/File.h"
    "include/Sinks/Sink.h"
    "include/Sinks/StdOut.h"
)
source_group("Headers" FILES ${Headers})

set(Sources
    "external/fmt/src/format.cc"
    "external/fmt/src/posix.cc"
    "src/Details/LoggingFunction.cpp"
    "src/Sinks/File.cpp"
    "src/Sinks/Sink.cpp"
    "src/Sinks/StdOut.cpp"
)
source_group("Sources" FILES ${Sources})

set(ALL_FILES
    ${Headers}
    ${Sources}
)

################################################################################
# Target
################################################################################
add_library(${PROJECT_NAME} STATIC ${ALL_FILES})
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Libraries")


set(ROOT_NAMESPACE BasicLogger)

################################################################################
# Output directory
################################################################################
set_target_properties(${PROJECT_NAME} PROPERTIES
    OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/build/${PROJECT_NAME}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/bin/"
    OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/build/${PROJECT_NAME}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/bin/"
    OUTPUT_DIRECTORY_TEST    "${CMAKE_SOURCE_DIR}/build/${PROJECT_NAME}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/bin/"
)
set_target_properties(${PROJECT_NAME} PROPERTIES
    INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    INTERPROCEDURAL_OPTIMIZATION_TEST    "TRUE"
)
################################################################################
# Include directories
################################################################################
target_include_directories(${PROJECT_NAME} PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/include;"
    "${CMAKE_CURRENT_SOURCE_DIR}/external/fmt/include"
)

################################################################################
# Compile definitions
################################################################################
target_compile_definitions(${PROJECT_NAME} PRIVATE
    "_CRT_SECURE_NO_WARNINGS;"
    "COF_USE_LOGGER;"
    "_MBCS"
)

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE
        $<$<CONFIG:Debug>:
            /Od;
            ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
        >
        $<$<CONFIG:Release>:
            /O2;
            /Oi;
            ${DEFAULT_CXX_RUNTIME_LIBRARY};
            /Gy
        >
        $<$<CONFIG:Test>:
            /O2;
            /Oi;
            ${DEFAULT_CXX_RUNTIME_LIBRARY};
            /Gy
        >
        /permissive-;
        /std:c++17;
        /sdl;
        /W3;
        ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
        ${DEFAULT_CXX_EXCEPTION_HANDLING}
    )
    target_link_options(${PROJECT_NAME} PRIVATE
        $<$<CONFIG:Release>:
            /OPT:REF;
            /OPT:ICF
        >
        $<$<CONFIG:Test>:
            /OPT:REF;
            /OPT:ICF
        >
    )
endif()
