cmake_minimum_required(VERSION 3.9.0)
SET(PROJECT_NAME "occSketcher")
project(${PROJECT_NAME})
set(default_build_type "Release")

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


# Find opencascade libraries

if(Qt5_DIR)
  find_package(Qt5 COMPONENTS Core REQUIRED)
  find_package(Qt5 COMPONENTS Gui Help OpenGL PrintSupport Svg Widgets QUIET)
  string(REPLACE "/lib/cmake/Qt5" "" Qt_ROOT_DIR ${Qt5_DIR})
elseif(Qt6_DIR)
  find_package(Qt6 COMPONENTS Core REQUIRED)
  find_package(Qt6 COMPONENTS Gui Help OpenGL PrintSupport Svg Widgets QUIET)
  string(REPLACE "/lib/cmake/Qt6" "" Qt_ROOT_DIR ${Qt6_DIR})
endif() 

set(QT_INCLUDE_DIR ${Qt_ROOT_DIR}/include
                   ${Qt_ROOT_DIR}/include/QtCore
                   ${Qt_ROOT_DIR}/include/QtGui
                   ${Qt_ROOT_DIR}/include/QtHelp
                   ${Qt_ROOT_DIR}/include/QtOpenGL
                   ${Qt_ROOT_DIR}/include/QtPrintSupport
                   ${Qt_ROOT_DIR}/include/QtSql
                   ${Qt_ROOT_DIR}/include/QtSvg
                   ${Qt_ROOT_DIR}/include/QtWidgets)         

find_package(OpenCASCADE COMPONENTS FoundationClasses REQUIRED)
find_package(OpenCASCADE COMPONENTS ModelingAlgorithms REQUIRED)
find_package(OpenCASCADE COMPONENTS ModelingData REQUIRED)
find_package(OpenCASCADE COMPONENTS DataExchange REQUIRED)
find_package(OpenCASCADE COMPONENTS Visualization REQUIRED)


set(MY_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(MY_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

include_directories(${MY_INCLUDE_DIR} ${OpenCASCADE_INCLUDE_DIR} ${QT_INCLUDE_DIR})

link_directories(${OpenCASCADE_LIBRARY_DIR})

set(occSketcher_SRC
Geom2d_Arc.cxx
Geom2d_Edge.cxx
Sketcher_AnalyserSnap.cxx
Sketcher_CommandArc3P.cxx
Sketcher_CommandArcCenter2P.cxx
Sketcher_CommandBezierCurve.cxx
Sketcher_CommandCircle2PTan.cxx
Sketcher_CommandCircle3P.cxx
Sketcher_CommandCircle3Tan.cxx
Sketcher_CommandCircleCenterRadius.cxx
Sketcher_CommandCircleP2Tan.cxx
Sketcher_Command.cxx
Sketcher_CommandLine2P.cxx
Sketcher_CommandPoint.cxx
Sketcher_CommandTrim.cxx
Sketcher.cxx
#Sketcher_GUI.cxx
Sketcher_Object.cxx
Sketcher_PropertyArc.cxx
Sketcher_PropertyCircle.cxx
Sketcher_Property.cxx
Sketcher_PropertyLine.cxx
Sketcher_PropertyPoint.cxx
#Sketcher_QtGUI.cxx
Sketcher_SnapCenter.cxx
Sketcher_Snap.cxx
Sketcher_SnapEnd.cxx
Sketcher_SnapIntersection.cxx
Sketcher_SnapLine.cxx
Sketcher_SnapLineParallel.cxx
Sketcher_SnapLinePerpendicular.cxx
Sketcher_SnapMiddle.cxx
Sketcher_SnapNearest.cxx
Sketcher_SnapTangent.cxx)
  
message(STATUS "mis fuentes -- ${occSketcher_SRC}")
add_library(occSketcher MODULE ${occSketcher_SRC})
target_link_libraries(occSketcher ${OpenCASCADE_LIBRARIES})  
