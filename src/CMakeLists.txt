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
