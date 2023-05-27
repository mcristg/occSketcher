cmake_minimum_required(VERSION 3.9.0)
SET(PROJECT_NAME "occSketcher")
project(${PROJECT_NAME})
set(default_build_type "Release")


if(Qt5_DIR)
  set(CMAKE_CXX_STANDARD 14)
  find_package(Qt5 COMPONENTS Core REQUIRED)
  find_package(Qt5 COMPONENTS Gui Help OpenGL PrintSupport Svg Widgets QUIET)
  string(REPLACE "/lib/cmake/Qt5" "" Qt_ROOT_DIR ${Qt5_DIR})
elseif(Qt6_DIR)
  set(CMAKE_CXX_STANDARD 17)
  string(REPLACE "Qt6" "Qt6CoreTools" Qt6CoreTools_DIR ${Qt6_DIR})
  string(REPLACE "Qt6" "Qt6GuiTools" Qt6GuiTools_DIR ${Qt6_DIR})
  string(REPLACE "Qt6" "Qt6WidgetsTools" Qt6WidgetsTools_DIR ${Qt6_DIR})
  string(REPLACE "Qt6" "Qt6DBusTools" Qt6DBusTools_DIR ${Qt6_DIR})
  find_package(Qt6 COMPONENTS Core REQUIRED)
  find_package(Qt6 COMPONENTS Gui Help OpenGL PrintSupport Svg Widgets QUIET)
  string(REPLACE "/lib/cmake/Qt6" "" Qt_ROOT_DIR ${Qt6_DIR})
endif() 

set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(QT_INCLUDE_DIR ${Qt_ROOT_DIR}/include
                   ${Qt_ROOT_DIR}/include/QtCore
                   ${Qt_ROOT_DIR}/include/QtGui
                   ${Qt_ROOT_DIR}/include/QtHelp
                   ${Qt_ROOT_DIR}/include/QtOpenGL
                   ${Qt_ROOT_DIR}/include/QtPrintSupport
                   ${Qt_ROOT_DIR}/include/QtSql
                   ${Qt_ROOT_DIR}/include/QtSvg
                   ${Qt_ROOT_DIR}/include/QtWidgets)
                       
# Find opencascade libraries

find_package(OpenCASCADE COMPONENTS FoundationClasses REQUIRED)
find_package(OpenCASCADE COMPONENTS ModelingAlgorithms REQUIRED)
find_package(OpenCASCADE COMPONENTS ModelingData REQUIRED)
find_package(OpenCASCADE COMPONENTS DataExchange REQUIRED)
find_package(OpenCASCADE COMPONENTS Visualization REQUIRED)


set(MY_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(MY_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(src)

