cmake_minimum_required(VERSION 3.5)

project(lenet_trt)

set(CMAKE_CXX_STANDARD 14)

# CUDA
set(my_cuda_dir /home/chaomath/cuda-10.2/16.04)
set(CUDA_TOOLKIT_ROOT_DIR ${my_cuda_dir})
find_package(CUDA 10.2 REQUIRED)
include_directories(${my_cuda_dir}/include)
link_directories(${my_cuda_dir}/lib)
message(STATUS "Find CUDA include at ${CUDA_INCLUDE_DIRS}")
message(STATUS "Find CUDA libraries: ${CUDA_LIBRARIES}")

# TensorRT
set(my_trt_dir /home/chaomath/TensorRT-7.0.0)
set(TENSORRT_ROOT ${my_trt_dir})
include_directories(${my_trt_dir}/include)
link_directories(${my_trt_dir}/lib)
message(STATUS "Found TensorRT headers at ${TENSORRT_INCLUDE_DIR}")
message(STATUS "Find TensorRT libs: ${TENSORRT_LIBRARY}")

# OpenCV
set(my_cv_dir /home/chaomath/opencv-3.4.9/build)
set(OpenCV_DIR ${my_cv_dir})
find_package(OpenCV REQUIRED)
#include_directories(${OpenCV_INCLUDE_DIRS})
message(STATUS "Find OpenCV include at ${OpenCV_INCLUDE_DIRS}")
message(STATUS "Find OpenCV libraries: ${OpenCV_LIBRARIES}")

# YAML
set(YAML_INCLUDE ./yaml-cpp/include)
set(YAML_LIB_DIR ./yaml-cpp/libs)
include_directories(${YAML_INCLUDE})
link_directories(${YAML_LIB_DIR})
message(STATUS "Find YAML include at ${YAML_INCLUDE}")
message(STATUS "Find YAML libraries: ${YAML_LIB_DIR}")

# self file
include_directories(./includes)

add_executable(lenet_trt main.cpp lenet.cpp model.cpp common.cpp)

target_link_libraries(lenet_trt cudart cublas)
target_link_libraries(lenet_trt nvinfer nvonnxparser)
target_link_libraries(lenet_trt yaml-cpp)
target_link_libraries(lenet_trt ${OpenCV_LIBRARIES})

