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

