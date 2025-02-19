cmake_minimum_required(VERSION 2.8)

project(tracker)
  
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O3")
if(CMAKE_COMPILER_IS_GNUCXX)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wextra -pedantic -Wno-long-long")
endif()

#寻找OpenCV库
#修改成捏OpenCV路径即可
set(OpenCV_DIR ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/opencv/x64/vc14/lib)
set(OpenCV_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/opencv/include) 
find_package(OpenCV REQUIRED)

if (OPENMP_FOUND)
    message("OpenMP found!")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/ncnn/include)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/ncnn/debug)

add_executable(MultiFaceTracking main.cpp mtcnn.cpp colotracker.cpp)
target_link_libraries(MultiFaceTracking ncnn ${OpenCV_LIBS}  -fopenmp)





