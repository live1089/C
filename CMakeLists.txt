# 设置 CMake 的最低版本
cmake_minimum_required(VERSION 3.10)

# 定义项目名称和使用的语言
project(WebCMake LANGUAGES C)

# 设置 C 标准
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# 如果未设置构建类型，则设置为 Debug
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug CACHE STRING "Build type" FORCE)
endif()

# 自动收集 src/ 目录下的所有 .c 文件
file(GLOB SRC_FILES ${CMAKE_SOURCE_DIR}/src/*.c)

# 如果未找到源文件，则报错
if(NOT SRC_FILES)
    message(FATAL_ERROR "No source files found in ${CMAKE_SOURCE_DIR}/src/")
endif()

# 检查 Inc/ 目录是否存在
if(NOT EXISTS ${CMAKE_SOURCE_DIR}/Inc)
    message(FATAL_ERROR "Include directory ${CMAKE_SOURCE_DIR}/Inc does not exist!")
endif()

# 添加可执行文件
add_executable(web_program ${SRC_FILES})

# 设置头文件目录（仅针对 web_program）
target_include_directories(web_program PRIVATE ${CMAKE_SOURCE_DIR}/Inc)

