# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_LIB_SRCS 变量
aux_source_directory(. DIR_LIB_SRCS)

#设置输出路径
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

# 生成动态链接库SHARED 静态库STATIC
add_library (MathFunctions SHARED ${DIR_LIB_SRCS})

# 指定 MathFunctions 库的安装路径
install (TARGETS MathFunctions DESTINATION /home/pi/Desktop/rr/Test_Demo6/lib)
install (FILES MathFunctions.h DESTINATION /home/pi/Desktop/rr/Test_Demo6/include)