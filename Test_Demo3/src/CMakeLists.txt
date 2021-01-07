
#包含的文件路径
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/MyMath)

#设置输出文件的路径
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

# 查找当前目录显得所有源文件
#并将名称保存到DIR_SRCS的变量中 
aux_source_directory(. DIR_SRCS)

#指定生成目标
add_executable(Demo3 main.cpp)

#添加链接库
target_link_libraries(Demo3 MathFunctions)