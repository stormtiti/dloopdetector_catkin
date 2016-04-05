cmake_minimum_required(VERSION 2.8.3)
project(dloopdetector_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(dloopdetector_src
  GIT_REPOSITORY git@github.com:dorian3d/DLoopDetector.git
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
  PATCH_COMMAND cd ../dloopdetector_src && git apply ${CMAKE_CURRENT_SOURCE_DIR}/includes.patch
)
ExternalProject_CatkinInstall(dloopdetector_src)

cs_install()
cs_export(
  INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
  CFG_EXTRAS dloopdetector-extras.cmake)
