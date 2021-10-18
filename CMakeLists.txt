cmake_minimum_required(VERSION 3.20)

set(PROJECT_NAME transformation)
cmake_policy(SET CMP0048 NEW)
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 20)
message(${CMAKE_SOURCE_DIR})

# 设定可执行二进制文件的目录
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# 设定存放编译出来的库文件的目录
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# 并且把该目录设为连接目录
link_directories(
        D:/clibs/AzureKinectSDK/1.4.1/sdk/windows-desktop/amd64/release/lib
)
# 日志
set(SPDLOG_INCLUDE D:/clibs/spdlog/1.9.2/include)
# opencv
set(OPENCV_INCLUDE D:/clibs/opencv/4.5.3/include)
set(OPENCV_LIB D:/clibs/opencv/4.5.3/x64/mingw/bin)
# kinect
set(KINECT_INCLUDE D:/clibs/AzureKinectSDK/1.4.1/sdk/include)
set(KINECT_LIB D:/clibs/AzureKinectSDK/1.4.1/sdk/windows-desktop/amd64/release/bin)
# libjpeg-turbo
set(LIBJPEG_TURBO_INCLUDE D:/clibs/libjpeg-turbo-vc64/2.1.1/include)
set(LIBJPEG_TURBO_LIB D:/clibs/libjpeg-turbo-vc64/2.1.1/bin)

include_directories(
        ${SPDLOG_INCLUDE}
        ${OPENCV_INCLUDE}
        ${KINECT_INCLUDE}
        ${LIBJPEG_TURBO_INCLUDE}
)


add_executable(${PROJECT_NAME} main.cpp transformation_helpers.cpp transformation_helpers.h)

target_include_directories(${PROJECT_NAME} PRIVATE
        ${SPDLOG_INCLUDE}
        ${OPENCV_INCLUDE}
        ${KINECT_INCLUDE}
        ${LIBJPEG_TURBO_INCLUDE}
        )

target_link_libraries(${PROJECT_NAME} PRIVATE
        ${KINECT_LIB}/k4a.dll
        ${KINECT_LIB}/k4arecord.dll
        ${OPENCV_LIB}/libopencv_core453.dll
        ${OPENCV_LIB}/libopencv_highgui453.dll
        ${OPENCV_LIB}/libopencv_imgcodecs453.dll
        ${OPENCV_LIB}/libopencv_imgproc453.dll
        ${OPENCV_LIB}/libopencv_objdetect453.dll
        ${LIBJPEG_TURBO_LIB}/turbojpeg.dll
        )
