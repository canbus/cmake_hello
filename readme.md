# windows cmake + mingw 环境搭建
1. 安装cmake. 下载:https://cmake.org/download/
2. 验证cmake,在power shell中输入cmake,没有出错表示成功
    ```
    PS C:\Users\hp> cmake
    Usage ...
    ```
3. 安装mingw. 下载:https://sourceforge.net/projects/mingw-w64/
4. 验证,在power shell中输入gcc,要能看到输出表示成功
    ```
    PS C:\Users\hp> gcc
    gcc.exe: fatal error: no input files
    compilation terminated
    ```
5. 找到mingw安装目录下mingw32-make.exe拷贝一份并重命名为make.exe
6. 编写main.c
```c
#include <stdlib.h>
void main()
{
    printf("hello cmake\n");
}
```
7. 编写CMake文件"CMakeLists.txt"
```
cmake_minimum_required(VERSION 3.0)
project(Hello)
set(SOURCE main.c)
add_executable(${PROJECT_NAME} ${SOURCE})
```
8. 生成Make file
```
mkdir build
cd build
cmake -G"Unix Makefiles" ../
```
9. make

# cmake实例
## 基本操作流程
1. $> cmake directory
2. $> make
## cmake示例(CMake的命令全部为大写)
```camke简单示例(CMakeLists.txt)
cmake_minimum_required(VERSION 3.0)

project(Hello) #指定工程名

INCLUDE_DIRECTORIES(include  )  #指定头文件

AUX_SOURCE_DIRECTORY(. SRCS_LIST)  #指定源文件目录

add_executable(${PROJECT_NAME} ${SRCS_LIST}) #添加一个可执行文件构建目标
```

````camke多目录示例(CMakeLists.txt)
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
```

```cmake示例
#project name  
PROJECT(test_math)  #指定工程名
  
add_definitions("-Wall -lpthread -g")  
  
#head file path     #指定头文件目录为include
INCLUDE_DIRECTORIES( include )  
  
#source directory   #指定源文件目录为src，并将其赋值给环境变量DIR_SRCS
AUX_SOURCE_DIRECTORY(src DIR_SRCS)  
  
#set environment variable  #设定环境变量TEST_MATH的值为环境变量DIR_SRCS的值
SET(TEST_MATH  
${DIR_SRCS}  
)  
  
#set extern libraries  #将libm.so赋值给环境变量LIBRARIES
SET(LIBRARIES  
libm.so  
)  
  
# set output binary path  
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)  
  
SET(FS_BUILD_BINARY_PREFIX "Yfs")  
  
#add executable file  
ADD_EXECUTABLE(${FS_BUILD_BINARY_PREFIX}sqrt ${TEST_MATH})  
  
#add link library  
TARGET_LINK_LIBRARIES(${FS_BUILD_BINARY_PREFIX}sqrt ${LIBRARIES})  
```


##
echo "# cmake_hello" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/canbus/cmake_hello.git
git push -u origin main