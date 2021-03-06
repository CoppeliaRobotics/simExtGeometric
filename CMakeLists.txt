cmake_minimum_required(VERSION 3.15)
project(simExtGeom)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_MACOSX_RPATH 1)

find_package(Boost REQUIRED)

if(NOT LIBPLUGIN_DIR)
    if(DEFINED ENV{COPPELIASIM_ROOT_DIR})
        set(LIBPLUGIN_DIR $ENV{COPPELIASIM_ROOT_DIR}/programming/libPlugin)
    else()
        set(LIBPLUGIN_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../libPlugin)
    endif()
endif()
list(APPEND CMAKE_MODULE_PATH ${LIBPLUGIN_DIR}/cmake)
find_package(CoppeliaSim 4.1.0.0 REQUIRED)

coppeliasim_add_plugin(
    simExtGeom
    LEGACY
    SOURCES
    simExtGeom.cpp
    ../coppeliaGeometricRoutines/geom.cpp
    ../coppeliaGeometricRoutines/calcUtils.cpp
    ../coppeliaGeometricRoutines/obbNode.cpp
    ../coppeliaGeometricRoutines/obbStruct.cpp
    ../coppeliaGeometricRoutines/ocNode.cpp
    ../coppeliaGeometricRoutines/ocStruct.cpp
    ../coppeliaGeometricRoutines/pcNode.cpp
    ../coppeliaGeometricRoutines/pcStruct.cpp
    ../coppeliaGeometricRoutines/kdNode.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/MyMath.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/3Vector.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/4Vector.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/7Vector.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/3X3Matrix.cpp
    ${COPPELIASIM_ROOT_DIR}/programming/simMath/4X4Matrix.cpp
    ${COPPELIASIM_COMMON_DIR}/scriptFunctionData.cpp
    ${COPPELIASIM_COMMON_DIR}/scriptFunctionDataItem.cpp
)
target_compile_definitions(simExtGeom PRIVATE SIM_MATH_DOUBLE)
target_include_directories(simExtGeom PRIVATE ../coppeliaGeometricRoutines)
target_include_directories(simExtGeom PRIVATE ${COPPELIASIM_ROOT_DIR}/programming/simMath)
coppeliasim_add_helpfile(simGeom.htm)
coppeliasim_add_helpfile(simGeom.json SUBDIR index)
