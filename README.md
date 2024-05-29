# CoreMP135_framebuffer_OpenCV

CoreMP135で、LCDとDisplayPortに画像を表示するサンプルです。ライブラリにはOpenCV-Mobileを使っています。

This is a sample that displays images on LCD and DisplayPort using coremp135. I am using OpenCV-Mobile as the library.



### Install

```
$ wget https://www.eizo.co.jp/eizolibrary/other/itmedia04/06b.jpg
$ sudo apt install arm-linux-gnueabihf-g++ arm-linux-gnueabihf-gcc cmake
$ git clone https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV.git
$ cd CoreMP135_framebuffer_OpenCV
$ mkdir build
$ cd build
$ cmake ..
$ make
```

### result in CoreMP135
Copy the generated binary to CoreMP135 and run it.

```
nnn@M5Core135:/home/share$ sudo ./frame_buffer_opencv
/dev/fb0 information
--------------------------
Frame Buffer Device Information:
ID: stmdrmfb
Memory Length: 1843200 bytes
Type: 0
Type Aux: 0
Visual: 2
Line Length: 2560 bytes per line
--------------------------
Variable Framebuffer Information:
Resolution: 1280x720
Virtual Resolution: 1280x720
Bits Per Pixel: 16
Red: Offset 11, Length 5
Green: Offset 5, Length 6
Blue: Offset 0, Length 5
--------------------------
/dev/fb1 information
--------------------------
Frame Buffer Device Information:
ID: fb_ili9341
Memory Length: 153600 bytes
Type: 0
Type Aux: 0
Visual: 2
Line Length: 640 bytes per line
--------------------------
Variable Framebuffer Information:
Resolution: 320x240
Virtual Resolution: 320x240
Bits Per Pixel: 16
Red: Offset 11, Length 5
Green: Offset 5, Length 6
Blue: Offset 0, Length 5
--------------------------
```


