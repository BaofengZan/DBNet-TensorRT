cmake_minimum_required(VERSION 2.6)

project(yolov5)

add_definitions(-std=c++11)

option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)

#设置cuda信息
find_package(CUDA REQUIRED)

message(STATUS "    libraries: ${CUDA_LIBRARIES}")
message(STATUS "    include path: ${CUDA_INCLUDE_DIRS}")
include_directories(${CUDA_INCLUDE_DIRS})
set(CUDA_NVCC_PLAGS ${CUDA_NVCC_PLAGS};-std=c++11; -g; -G;-gencode; arch=compute_75;code=sm_75)
enable_language(CUDA)  # 这一句添加后 ，就会在vs中不需要再手动设置cuda 

include_directories(${PROJECT_SOURCE_DIR}/include)

include_directories(D:\\TensorRT-7.0.0.11.Windows10.x86_64.cuda-10.2.cudnn7.6\\TensorRT-7.0.0.11\\include)

#-D_MWAITXINTRIN_H_INCLUDED  解决error: identifier "__builtin_ia32_mwaitx" is undefined
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Ofast -D_MWAITXINTRIN_H_INCLUDED")

# 设置opencv的信息
set(OpenCV_DIR "D:\\opencv\\opencv346\\build")
find_package(OpenCV QUIET
    NO_MODULE
    NO_DEFAULT_PATH
    NO_CMAKE_PATH
    NO_CMAKE_ENVIRONMENT_PATH
    NO_SYSTEM_ENVIRONMENT_PATH
    NO_CMAKE_PACKAGE_REGISTRY
    NO_CMAKE_BUILDS_PATH
    NO_CMAKE_SYSTEM_PATH
    NO_CMAKE_SYSTEM_PACKAGE_REGISTRY
)

message(STATUS "OpenCV library status:")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

include_directories(${OpenCV_INCLUDE_DIRS})

link_directories(D:\\TensorRT-7.0.0.11.Windows10.x86_64.cuda-10.2.cudnn7.6\\TensorRT-7.0.0.11\\lib)

add_executable(dbnet ${PROJECT_SOURCE_DIR}/dbnet.cpp)

target_link_libraries(dbnet "nvinfer" "nvinfer_plugin" "nvparsers" "nvonnxparser")
#target_link_libraries(dbnet "cudart")
target_link_libraries(dbnet ${OpenCV_LIBS})
target_link_libraries(dbnet ${CUDA_LIBRARIES})

add_definitions(-pthread)

