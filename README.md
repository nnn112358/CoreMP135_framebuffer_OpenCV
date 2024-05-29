# CoreMP135_framebuffer_OpenCV

CoreMP135で、LCDとDisplayPort(HDMI)に画像を表示するサンプルです。ライブラリにはOpenCV-Mobileを使っています。
This is a sample that displays images on LCD and DisplayPort using coremp135. I am using OpenCV-Mobile as the library.

The following color conversion is required in CoreMP135.  
CoreMP135では、以下の色変換が必要です。  DisplayPortとLCDとで、BチャンネルとRチャンネルを逆にする必要があります。
DisplayPort(HDMI):BGR888⇒RGB565  
LCD:BGR888⇒BGR565  

また、デフォルトでは以下の解像度になります。  
In addition, the default resolution is as follows.  
DisplayPort(HDMI): 1280x720  
LCD:320x240  



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

# Referrence


