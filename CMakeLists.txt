cmake_minimum_required(VERSION 3.0)

project(Hello)

INCLUDE_DIRECTORIES(  
include  
)  

AUX_SOURCE_DIRECTORY(. SRCS_LIST)  


add_executable(${PROJECT_NAME} ${SRCS_LIST})