project(android-libnativehelper)

# Carl HACK
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fpermissive")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive")

include_directories(
  include/nativehelper
)

set(SRC
  JNIHelp.cpp
)

add_library(android-libnativehelper OBJECT ${SRC})
set(LIBNATIVEHELPER_OBJECTS $<TARGET_OBJECTS:android-libnativehelper> PARENT_SCOPE)

