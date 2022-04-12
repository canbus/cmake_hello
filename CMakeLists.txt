cmake_minimum_required(VERSION 3.0)

project(Hello ) #指定工程名

add_definitions("-Wall -lpthread -g")  

set(CMAKE_C_STANDARD 11) 

INCLUDE_DIRECTORIES(inc  )  #指定头文件目录

AUX_SOURCE_DIRECTORY(src SRCS_LIST)  #指定源文件目录1
AUX_SOURCE_DIRECTORY(drv SRCS_LIST)  #指定源文件目录2

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)  #设置可执行文件的输出路径

add_executable(${PROJECT_NAME} ${SRCS_LIST}) #添加一个可执行文件构建目标

# file(COPY ${PROJECT_NAME}  DESTINATION ../${PROJECT_NAME}   ) #文件拷贝

# 使用步骤(在build目录下)
# 1.生成makefile: build> cmake -G "Unix Makefiles" ..\
# 2.生成目标程序 : build> make