# Generated from MQ2EasyFind.vcxproj
# This file is designed to work with add_subdirectory()

# ---------------------------------------------------------------------
# Props file includes
# ---------------------------------------------------------------------
include("../../src/Plugin.cmake")
find_package(luajit REQUIRED)
find_package(sol2 REQUIRED)

# ---------------------------------------------------------------------
# Header files
# ---------------------------------------------------------------------
set(MQ2EasyFind_HEADERS
    "EasyFind.h"
    "EasyFindConfiguration.h"
    "EasyFindWindow.h"
    "EasyFindZoneConnections.h"
    "resource.h"
)

source_groups("Header Files" ${MQ2EasyFind_HEADERS})

# ---------------------------------------------------------------------
# Other files
# ---------------------------------------------------------------------
set(MQ2EasyFind_OTHERFILES
    "MQ2EasyFind.rc"
    "README.md"
    "resources/EasyFind/ZoneConnections.yaml"
)

source_group("Resource Files" FILES ${MQ2EasyFind_OTHERFILES})

# ---------------------------------------------------------------------
# Assembly files
# ---------------------------------------------------------------------
set(MQ2EasyFind_ASSEMBLY
    "AssemblyFunctions.asm"
)

source_groups("Assembly Files" ${MQ2EasyFind_ASSEMBLY})

# ---------------------------------------------------------------------
# Source files
# ---------------------------------------------------------------------
set(MQ2EasyFind_SOURCES
    "EasyFind.cpp"
    "EasyFindConfiguration.cpp"
    "EasyFindImGui.cpp"
    "EasyFindNavigation.cpp"
    "EasyFindWindow.cpp"
    "EasyFindZoneConnections.cpp"
    "EasyFindZonePath.cpp"
)

source_groups("Source Files" ${MQ2EasyFind_SOURCES})

# ---------------------------------------------------------------------
# Target definition
# ---------------------------------------------------------------------
add_library(MQ2EasyFind SHARED
    ${MQ2EasyFind_HEADERS}
    ${MQ2EasyFind_OTHERFILES}
    ${MQ2EasyFind_ASSEMBLY}
    ${MQ2EasyFind_SOURCES}
)

set_target_properties(MQ2EasyFind PROPERTIES FOLDER "external")

# ---------------------------------------------------------------------
# Apply props file configurations
# ---------------------------------------------------------------------
target_Plugin_props(MQ2EasyFind)

# ---------------------------------------------------------------------
# Add NASM tool to ASM files
# ---------------------------------------------------------------------
add_nasm_sources(${MQ2EasyFind_ASSEMBLY})

# ---------------------------------------------------------------------
# Preprocessor definitions
# ---------------------------------------------------------------------
target_compile_definitions(MQ2EasyFind PRIVATE
    "SOL_LUAJIT=1"
)

# ---------------------------------------------------------------------
# Include directories
# ---------------------------------------------------------------------
target_include_directories(MQ2EasyFind PRIVATE
    "${CMAKE_CURRENT_LIST_DIR}/"
)

# ---------------------------------------------------------------------
# Link libraries
# ---------------------------------------------------------------------
target_link_libraries(MQ2EasyFind PRIVATE
    "$<$<CONFIG:Debug>:yaml-cppd.lib>"
    luajit::luajit
    sol2
    "$<$<CONFIG:Release>:yaml-cpp.lib>"
)

# ============================================================================
# MANUAL CONVERSION NOTES
# ============================================================================
#
# - Review and adjust as needed
