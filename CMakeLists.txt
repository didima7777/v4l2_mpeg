cmake_minimum_required(VERSION 2.8)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive")

project( Video )
find_package( OpenCV REQUIRED )

# V4L2
find_path(LIBV4L2_INCLUDE_DIR libv4l2.h)
if (NOT LIBV4L2_INCLUDE_DIR)
	message(STATUS "Could not find package V4L2. Try to install it")
	EXEC_PROGRAM("sudo apt-get install -y libv4l-dev")
	find_path(LIBV4L2_INCLUDE_DIR libv4l2.h)
endif (NOT LIBV4L2_INCLUDE_DIR)
include_directories(${LIBV4L2_INCLUDE_DIR}) 

find_library(LIBV4L2_LIBRARY v4l2)

add_executable( DisplayImage capture1.cpp )

target_link_libraries( DisplayImage  "${LIBV4L2_LIBRARY}" ${OpenCV_LIBS})