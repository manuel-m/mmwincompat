#==============================================================================
# CMake version minimum requirement
# 
#==============================================================================
cmake_minimum_required (VERSION 2.8) 

#==============================================================================
# mmwincompat
#==============================================================================
project (mmwincompat) 

#==============================================================================
# Additional package ressource finders
#==============================================================================
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/resources/CMake/Modules")

#==============================================================================
# The macro below forces the build directory to be different from source directory
#==============================================================================
include(MacroOutOfSourceBuild)
macro_ensure_out_of_source_build("${PROJECT_NAME} requires an out of source build.")

include(MacroLogAll)
macro_logall()

include(MacroDefineCFlags)
macro_define_cflags()

set(WC_DIST_DIR ${CMAKE_CURRENT_SOURCE_DIR}/dist)
file(MAKE_DIRECTORY ${WC_DIST_DIR})
set(EXECUTABLE_OUTPUT_PATH ${WC_DIST_DIR})
set(LIBRARY_OUTPUT_PATH ${WC_DIST_DIR})

#lib name definition
set( WC_LIB mmwincompat)

#debug release namming context
if (CMAKE_BUILD_TYPE MATCHES Debug)
  set(WC_LIB "${WC_LIB}_d")
endif (CMAKE_BUILD_TYPE MATCHES Debug)

include_directories (${CMAKE_CURRENT_SOURCE_DIR}/include )



file(GLOB wc_SOURCES *.c)
add_library (${WC_LIB} ${wc_SOURCES} )
