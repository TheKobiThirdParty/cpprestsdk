cmake_minimum_required(VERSION 3.9)
find_package(catkin REQUIRED COMPONENTS)
project(cpprest C CXX)

find_package(Threads REQUIRED)

set(cpprest_extras_LIBRARIES crypto boost_system)

catkin_package(
INCLUDE_DIRS
  Release/include
  Release/libs/websocketpp
LIBRARIES
  cpprest
DEPENDS cpprest_extras)

set(CPPREST_INSTALL_HEADERS ON CACHE BOOL "Enable system header install" FORCE)
set(CPPREST_INSTALL ON CACHE BOOL "Disable system library install" FORCE)
set(BUILD_TESTS OFF CACHE BOOL "Enable build tests" FORCE)
set(BUILD_SAMPLES OFF CACHE BOOL "Enable build samples" FORCE)
set(CPPREST_EXCLUDE_WEBSOCKETS ON CACHE BOOL "Exclude websockets functionality." FORCE)

add_subdirectory(Release)

# Installs websocketpp headers which is not installed by cpprestsdk
install(
  DIRECTORY Release/libs/websocketpp/websocketpp
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING
  PATTERN "*.h*")

# Targets are installed properly in the catkin folder with
