# fips-ChromaTag/CMakeLists.txt

cmake_minimum_required(VERSION 3.10)

# use FIPS_ROOT from environment
get_filename_component(FIPS_ROOT_DIR "$ENV{FIPS_ROOT}" ABSOLUTE)
if(FIPS_ROOT_DIR)
    set(FIPS_ROOT_DIR "${FIPS_ROOT_DIR}/fips")
else(FIPS_ROOT_DIR)
    set(FIPS_ROOT_DIR "../fips")
endif(FIPS_ROOT_DIR)

# include the fips main cmake file
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

set(FIPS_RTTI OFF)

#Windows: build static lib with static CRT to be consistent. This avoids obscure errors. 
if(MSVC)
	set(BUILD_SHARED_LIBS OFF)
	set(BUILD_WITH_STATIC_CRT ON)
else()
	set(CMAKE_BUILD_TYPE RELEASE)
endif()
set(CMAKE_CXX_FLAGS "-std=c++14")

project(fips-ChromaTag)
# set(LCM_FOUND OFF)
fips_add_subdirectory(ChromaTag)
