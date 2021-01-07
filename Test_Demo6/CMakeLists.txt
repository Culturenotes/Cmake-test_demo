# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Test_Demo6)

#调用环境变量的方式自动添加 CMAKE_CURRENT_BINARY_DIR 和 CMAKE_CURRENT_SOURCE_DIR 到当前处理
#的 CMakeLists.txt。相当于在每个 CMakeLists.txt 加入:INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})

set (CMAKE_INCLUDE_CURRENT_DIR ON)

#CMake 支持 gdb 的设置
set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

# 设置c++的版本并添加多线程的使用
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -pthread")


ADD_SUBDIRECTORY(./MyMath)

ADD_SUBDIRECTORY(./src)


# 指定安装路径 默认在usr/local/路径下边
install (TARGETS Demo6 DESTINATION /home/pi/Desktop/rr/Test_Demo6/bin)
install (FILES "${PROJECT_BINARY_DIR}/config/config.hpp"
         DESTINATION /home/pi/Desktop/rr/Test_Demo6/include)

# 启用测试
enable_testing()

# 测试程序是否成功运行
add_test (test_run ./bin/Demo6 5 2)

# 定义一个宏，用来简化测试工作
macro (do_test arg1 arg2 result)
  add_test (test_${arg1}_${arg2} ./bin/Demo6 ${arg1} ${arg2})
  set_tests_properties (test_${arg1}_${arg2}
    PROPERTIES PASS_REGULAR_EXPRESSION ${result})
endmacro (do_test)

# 利用 do_test 宏，测试一系列数据
do_test (5 2 "is 25")
do_test (10 5 "is 100000")
do_test (2 10 "is 1024")