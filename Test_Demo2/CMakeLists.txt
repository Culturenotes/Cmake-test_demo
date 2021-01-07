# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Test_Demo2)

# 设置c++的版本并添加多线程的使用
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -pthread")

# 查找当前目录显得所有源文件
#并将名称保存到DIR_SRCS的变量中 
aux_source_directory(. DIR_SRCS)

#指定生成目标
add_executable(Demo2 ${DIR_SRCS})