# プロジェクト名と使用言語、CMakeの最低バージョンを設定
cmake_minimum_required(VERSION 3.5)
project(example LANGUAGES CXX)

# ビルドタイプをリリースに設定して、最適化されたパフォーマンスでビルド
set(CMAKE_BUILD_TYPE Release)

# コンパイラとC++標準を設定
set(CMAKE_CXX_COMPILER arm-linux-gnueabihf-g++)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# デバッグとリリースビルドのコンパイラフラグ
set(CMAKE_CXX_FLAGS_DEBUG "-O0 -Wall -g2 -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall")

# OpenCVの設定
SET(OpenCV_DIR /opt/opencv/opencv-mobile-4.10.0-armlinux/arm-linux-gnueabihf/lib/cmake/opencv4)

find_package(OpenCV REQUIRED)

# OpenCVが見つかった場合の情報出力
if(OpenCV_FOUND)
  message("OpenCV version: ${OpenCV_VERSION}")
  message(STATUS "OpenCV_LIBS: ${OpenCV_LIBS}")
  message(STATUS "OpenCV_INCLUDE_DIRS: ${OpenCV_INCLUDE_DIRS}")
endif()

# 実行可能ファイルを設定し、ソースファイルを追加
add_executable(frame_buffer_opencv main.cpp)

# OpenCVとプロジェクトのインクルードディレクトリを設定
target_include_directories(frame_buffer_opencv PRIVATE ${PROJECT_SOURCE_DIR}/include ${OpenCV_INCLUDE_DIRS})

# OpenCVライブラリとリンク
target_link_libraries(frame_buffer_opencv PRIVATE ${OpenCV_LIBS})

