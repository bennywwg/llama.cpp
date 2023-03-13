cmake_minimum_required(VERSION 3.0.0)
project(llamacpp VERSION 0.1.0)

# C++ version 20
set(CMAKE_CXX_STANDARD 20)

add_subdirectory(AutoReflect)
add_custom_target(GenerateReflection COMMAND AutoReflect ${PROJECT_SOURCE_DIR}/Source/main.cpp)

add_executable(main
    Source/ggml.c
	Source/ggml.h
	Source/main.cpp
	Source/utils.cpp
	Source/utils.h
)

add_executable(quantize
    Source/ggml.c
	Source/ggml.h
	Source/quantize.cpp
	Source/utils.cpp
	Source/utils.h
)

target_include_directories(main PUBLIC ${PROJECT_SOURCE_DIR}/Source)
target_include_directories(main PUBLIC ${PROJECT_SOURCE_DIR}/AutoReflect/Include)
target_include_directories(main PUBLIC ${PROJECT_SOURCE_DIR}/AutoReflect/json/include)
add_dependencies(main GenerateReflection)