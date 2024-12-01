cmake_minimum_required(VERSION 3.16.3)
project(curr CXX)

# 指定 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
# 设置编译选项
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")

# 添加源文件目录
aux_source_directory(include SOURCE_FILES)
#定义两个变量，表示头文件路径和库路径
find_package(OpenSSL REQUIRED)
# 显示的包含头文件
include_directories(include)
if(OPENSSL_FOUND)
    add_executable(${PROJECT_NAME} ${SOURCE_FILES} test/main.cpp
            include/SHE.cpp
            include/SHE.h
            include/PHE.cpp
            include/PHE.h
    )

    target_include_directories(${PROJECT_NAME} PUBLIC include)
    # 链接 OpenSSL 库
    target_link_libraries(${PROJECT_NAME} OpenSSL::SSL OpenSSL::Crypto)

endif (OPENSSL_FOUND)

#cmake_minimum_required(VERSION 3.25)
#project(curr CXX)
#
#set(CMAKE_C_STANDARD 11)
## 设置编译选项
#set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
#
## 添加源文件目录
#set(OPENSSL_INCLUDE_DIR "D:\\OpenSSL-Win64\\include")
#set(OPENSSL_CRYPTO_LIBRARY "D:\\OpenSSL-Win64\\lib\\VC\\x64\\MT\\libcrypto_static.lib")
#set(OPENSSL_SSL_LIBRARY "D:\\OpenSSL-Win64\\lib\\VC\\x64\\MT\\libssl_static.lib")
#aux_source_directory(include SOURCE_FILES)
#aux_source_directory(test SOURCE_FILES)
#include_directories(include ${OPENSSL_INCLUDE_DIR})
#
#
#add_executable(${PROJECT_NAME} ${SOURCE_FILES} test/main.cpp
#        include/SHE.cpp
#        include/SHE.h
#        include/PHE.cpp
#        include/PHE.h
#)
#target_include_directories(${PROJECT_NAME} PUBLIC include)
## 链接 OpenSSL 库
#target_link_libraries(${PROJECT_NAME}  ${OPENSSL_SSL_LIBRARY} ${OPENSSL_CRYPTO_LIBRARY} ws2_32 Crypt32)
