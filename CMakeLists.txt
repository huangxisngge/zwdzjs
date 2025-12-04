cmake_minimum_required(VERSION 3.21)

project(PVZ LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_PREFIX_PATH "E:/qt/6.5.3/mingw_64/lib/cmake")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 找 Qt6
find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Gui Widgets Multimedia)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Gui Widgets Multimedia)

# 指定 Qt 安装路径
set(CMAKE_PREFIX_PATH "")

# 源文件和头文件
file(GLOB SRC_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)
file(GLOB HEADER_FILES ${CMAKE_CURRENT_SOURCE_DIR}/include/*.h)
set(RESOURCES ${CMAKE_CURRENT_SOURCE_DIR}/images.qrc)

# 使用 add_executable（更稳妥，避免 qt_add_executable 找不到）
if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    add_executable(PVZ
            main.cpp
            ${SRC_FILES}
            ${HEADER_FILES}
            ${RESOURCES}
    )

# 头文件目录
target_include_directories(PVZ PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

# 链接 Qt 库
target_link_libraries(PVZ PRIVATE
        Qt6::Core
        Qt6::Gui
        Qt6::Widgets
        Qt6::Multimedia
)
endif ()