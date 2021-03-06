CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

PROJECT(PYMESH_THIRD_PARTY)

# Set output directories
SET(INSTALL_PATH ${PROJECT_SOURCE_DIR}/../python/pymesh/third_party)
SET(LIBRARY_PATH ${INSTALL_PATH}/lib)
SET(INCLUDE_PATH ${INSTALL_PATH}/include)
MAKE_DIRECTORY(${INSTALL_PATH})
MAKE_DIRECTORY(${LIBRARY_PATH})
MAKE_DIRECTORY(${INCLUDE_PATH})

# Set install directory
SET(CMAKE_INSTALL_PREFIX ${INSTALL_PATH})

LINK_DIRECTORIES(/opt/local/lib)
LINK_DIRECTORIES(/usr/local/lib)
LINK_DIRECTORIES(/usr/lib)

# RPath
SET(CMAKE_MACOSX_RPATH ON)

# C++11
SET(CMAKE_CXX_STANDARD 11)

ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/cork)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/carve)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/eigen)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/quartet)
# Both eigen and qhull uses INCLUDE_INSTALL_DIR, unset to avoid collision.
UNSET(INCLUDE_INSTALL_DIR CACHE)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/tetgen)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/triangle)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/qhull)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/Clipper/cpp)

SET(BUILD_TESTING OFF CACHE BOOL "Enable/Disable continuous integration" FORCE)
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/mmg)

SET(CGAL_HEADER_ONLY ON CACHE BOOL "Enable the header only version of CGAL")
SET(WITH_examples OFF CACHE BOOL "No CGAL examples")
SET(WITH_demos OFF CACHE BOOL "No CGAL demos")
SET(WITH_tests OFF CACHE BOOL "No CGAL tests")
SET(WITH_CGAL_Qt5 OFF CACHE BOOL "NO Qt")
SET(WITH_CGAL_ImageIO OFF CACHE BOOL "NO CGAL Image")
ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/cgal)

LIST(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
SET(THIRD_PARTY_DIR ${PROJECT_SOURCE_DIR})
INCLUDE(geogram)

ADD_SUBDIRECTORY(${PROJECT_SOURCE_DIR}/draco)
SET(CGAL_DIR ${PROJECT_BINARY_DIR})
INCLUDE(TetWild)
