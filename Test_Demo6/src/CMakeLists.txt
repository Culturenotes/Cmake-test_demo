# 设置c++的版本并添加多线程的使用
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -pthread")

#设置输出文件的路径
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)


# 检查系统是否支持 pow 函数
include (${CMAKE_ROOT}/Modules/CheckFunctionExists.cmake)
check_function_exists (pow HAVE_POW)

# 加入一个配置头文件，用于处理 CMake 对源码的设置(输入，输出)
configure_file (
  "${PROJECT_SOURCE_DIR}/config/config.hpp.in"
  "${PROJECT_BINARY_DIR}/config/config.hpp"
  )

# 是否使用自己的 MathFunctions 库
option (USE_MYMATH
       "Use provided math implementation" ON)

# 是否加入 MathFunctions 库
if (USE_MYMATH)
  include_directories ("${PROJECT_SOURCE_DIR}/MyMath")
endif (USE_MYMATH)

# 查找当前目录显得所有源文件
#并将名称保存到DIR_SRCS的变量中 
aux_source_directory(./ DIR_SRCS)


#指定生成目标
add_executable(Demo6 ${DIR_SRCS})

#添加链接库
target_link_libraries(Demo6 MathFunctions)
