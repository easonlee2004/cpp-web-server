cmake_minimum_required(VERSION 3.10)
project(WebServer)

# 设置默认编译器
if(NOT CMAKE_CXX_COMPILER)
    set(CMAKE_CXX_COMPILER "g++")
endif()

# 设置调试选项
option(DEBUG "Enable debugging" ON)
if(DEBUG)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")
endif()

# 设置源文件列表
set(SOURCES
        main.cpp
        ./timer/lst_timer.cpp
        ./http/http_conn.cpp
        ./log/log.cpp
        ./CGImysql/sql_connection_pool.cpp
        webserver.cpp
        config.cpp
)

# 添加可执行文件目标
add_executable(server ${SOURCES})

# 链接库
target_link_libraries(server pthread mysqlclient)

# 添加清理目标
add_custom_target(clean COMMAND rm -f server)