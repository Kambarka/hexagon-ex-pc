# = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# CMAKE
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

set(SOLUTION_CMAKE_VERSION 3.25)
cmake_minimum_required(VERSION ${SOLUTION_CMAKE_VERSION})

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# PROJECT
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

set(HEXAGON_EX_VERSION 0.1.0)
project("HexagonEX" VERSION ${HEXAGON_EX_VERSION})

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# GLOBALS
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

set(SOLUTION_DIR ${CMAKE_SOURCE_DIR})
set(SOLUTION_SOURCES_DIR "${SOLUTION_DIR}/src")
set(HEXAGON_EX_OUTPUT_DIR "${SOLUTION_DIR}/bin")

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# CONFIGS
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  set(DEBUG ON)
  add_definitions(-DDEBUG=1)
else (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  set(DEBUG OFF)
endif (${CMAKE_BUILD_TYPE} STREQUAL "Debug")

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# SOURCES
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

set(SOLUTION_SOURCES
  "${SOLUTION_SOURCES_DIR}/main.cpp"
)

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# MODULES
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

# HexagonEX.Core
set(HEXAGON_EX_CORE_INCLUDE_DIR "${SOLUTION_SOURCES_DIR}/game/core/private")
add_subdirectory("${SOLUTION_SOURCES_DIR}/game/core")

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# BUILD
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

# Create Executable-Object
add_executable(exe ${SOLUTION_SOURCES})

# Configure Executable-Object
set_target_properties(exe PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${HEXAGON_EX_OUTPUT_DIR}"
  RUNTIME_OUTPUT_NAME "HexagonEX"
)

# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# LINK
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

# Link with Headers
target_include_directories(exe PRIVATE ${SOLUTION_SOURCES_DIR})

# HexagonEX.Core
target_link_libraries(exe
  hexagonex_core
)
target_include_directories(exe PRIVATE ${HEXAGON_EX_CORE_INCLUDE_DIR})

# = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
