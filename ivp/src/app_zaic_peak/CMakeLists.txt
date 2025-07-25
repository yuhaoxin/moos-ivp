#--------------------------------------------------------
# The CMakeLists.txt for:                   app_zaic_peak
# Author(s):                                Mike Benjamin
#--------------------------------------------------------

# Set System Specific Libraries
if (${WIN32})
  SET(SYSTEM_LIBS wsock32)
else (${WIN32})
  SET(SYSTEM_LIBS m)
endif (${WIN32})

if(CMAKE_SYSTEM_NAME STREQUAL Linux)
  SET(SYSTEM_LIBS ${SYSTEM_LIBS} GL)
endif(CMAKE_SYSTEM_NAME STREQUAL Linux)

SET(SRC
  ZAIC_PEAK_Model.cpp
  ZAIC_PEAK_GUI.cpp
  main.cpp
)
	  
ADD_EXECUTABLE(zaic_peak ${SRC})

TARGET_LINK_LIBRARIES(zaic_peak
  zaicview
  ivpbuild
  mbutil
  ivpcore
  ivpsolve
  fltk 
  fltk_gl
  dl
  ${SYSTEM_LIBS}
)

# http://developer.apple.com/qa/qa2007/qa1567.html
IF (${APPLE})
  SET_TARGET_PROPERTIES(zaic_peak PROPERTIES	  
    LINK_FLAGS "-framework OpenGL -framework AGL -framework Cocoa"
    )
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-cast-function-type ")
ENDIF (${APPLE})
