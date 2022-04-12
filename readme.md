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
## cmake命令(CMake的命令全部为大写)
```cmake
#project name  
PROJECT(test_math)  #指定工程名
  
add_definitions("-Wall -lpthread -g")  
  
#head file path     #指定头文件目录为include
INCLUDE_DIRECTORIES(  
include  
)  
  
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

