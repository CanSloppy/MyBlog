---
title: CMake常用命令
date: 2025-01-04 16:41:43
tags: 'Linux命令'
categories: 'Linux'
---

### 项目常用命令
```plain
cmake_minimum_required (VERSION 2.8)
project (learn_cmake)
add_executable(hello hello.cpp)
```

+ <font style="color:rgb(51, 51, 51);">第一行：cmake最低版本要求2.8，</font>
+ <font style="color:rgb(51, 51, 51);">第二行：本项目的工程名</font>
+ <font style="color:rgb(51, 51, 51);">第三行：第一个变量：要生成的可执行文件名为hello，后面的参数是需要的依赖。</font>

### <font style="color:rgb(51, 51, 51);">引用库命令</font>
```plain
set(FFMPEG4_DIR ${CMAKE_SOURCE_DIR}/3rdpart_lab/opencv_ffmpeg/win64/ffmpeg-6.1)
include_directories(${FFMPEG4_DIR}/include)
link_directories(${FFMPEG4_DIR}/lib)
```

+ <font style="color:rgb(51, 51, 51);">第一行：</font>设置地址
+ <font style="color:rgb(51, 51, 51);">第二行：</font>引用头文件
+ <font style="color:rgb(51, 51, 51);">第三行：</font>引用库

### 复制文件命令
```plain
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    "${CMAKE_CURRENT_SOURCE_DIR}/start.bat"
    "${CMAKE_BINARY_DIR}/")

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    "${CMAKE_CURRENT_SOURCE_DIR}/server"
    "${CMAKE_BINARY_DIR}/")
```

+ copy为复制单独文件命令
+ copy_directory为复制整个文件夹



### 链接需要用的库到项目
```plain
target_link_libraries(vehicle_station
    PRIVATE Qt${QT_VERSION_MAJOR}::Core Qt5::Quick
    Qt${QT_VERSION_MAJOR}::Widgets vehicle-client Qt${QT_VERSION_MAJOR}::Mqtt
    avcodec avutil avformat swscale libusb-1.0 hidapi
    ${OpenCV_LIBS}
)
```

+ 链接的库可以是qt的，自己的，第三方的

