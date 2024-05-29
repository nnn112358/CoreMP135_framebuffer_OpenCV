# �v���W�F�N�g���Ǝg�p����ACMake�̍Œ�o�[�W������ݒ�
cmake_minimum_required(VERSION 3.5)
project(example LANGUAGES CXX)

# �r���h�^�C�v�������[�X�ɐݒ肵�āA�œK�����ꂽ�p�t�H�[�}���X�Ńr���h
set(CMAKE_BUILD_TYPE Release)

# �R���p�C����C++�W����ݒ�
set(CMAKE_CXX_COMPILER arm-linux-gnueabihf-g++)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# �f�o�b�O�ƃ����[�X�r���h�̃R���p�C���t���O
set(CMAKE_CXX_FLAGS_DEBUG "-O0 -Wall -g2 -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall")

# OpenCV�̐ݒ�
#SET(OpenCV_DIR /home/nnn/LinuxHome/CoreMP135/opencv/opencv/install/arm/lib/cmake/opencv4/)
SET(OpenCV_DIR /home/nnn/LinuxHome/CoreMP135/opencv/opencv-mobile-4.9.0/install/arm/lib/cmake/opencv4/)

find_package(OpenCV REQUIRED)

# OpenCV�����������ꍇ�̏��o��
if(OpenCV_FOUND)
  message("OpenCV version: ${OpenCV_VERSION}")
  message(STATUS "OpenCV_LIBS: ${OpenCV_LIBS}")
  message(STATUS "OpenCV_INCLUDE_DIRS: ${OpenCV_INCLUDE_DIRS}")
endif()

# ���s�\�t�@�C����ݒ肵�A�\�[�X�t�@�C����ǉ�
add_executable(frame_buffer_opencv main.cpp)

# OpenCV�ƃv���W�F�N�g�̃C���N���[�h�f�B���N�g����ݒ�
target_include_directories(frame_buffer_opencv PRIVATE ${PROJECT_SOURCE_DIR}/include ${OpenCV_INCLUDE_DIRS})

# OpenCV���C�u�����ƃ����N
target_link_libraries(frame_buffer_opencv PRIVATE ${OpenCV_LIBS})
