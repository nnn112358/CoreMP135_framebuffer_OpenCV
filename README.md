# CoreMP135_framebuffer_OpenCV

CoreMP135で、LCDとDisplayPort(HDMI)に画像を表示するサンプルです。ライブラリにはOpenCV-Mobileを使っています。
This is a sample that displays images on LCD and DisplayPort using coremp135. I am using OpenCV-Mobile as the library.

CoreMP135では、画像データをframebudderに書き込む前に、以下の色変換が必要です。  DisplayPortとLCDとで、BチャンネルとRチャンネルを逆にする必要があります。
CoreMP135 requires the following color conversion before writing image data to framebudder. You need to reverse the B and R channels on DisplayPort and LCD.
DisplayPort(HDMI):BGR888⇒RGB565  
LCD:BGR888⇒BGR565  

また、デフォルトでは以下の解像度になります。  
In addition, the default resolution is as follows.  
DisplayPort(HDMI): 1280x720  
LCD:320x240  

<img width="640" alt="S__80977923" src="https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV/assets/27625496/7253fda7-6f79-4ebc-9a60-d4bf5b55b4bf">

## Enviroment

The firmware is "M5_CoreMP135_debian12_20240515"  
https://docs.m5stack.com/en/guide/linux/coremp135/image ⇒ M5_CoreMP135_debian12_20240515	

```
$ $user@M5Core135 $ uname -a
Linux M5Core135 5.15.118 #1 SMP PREEMPT Tue May 7 15:14:07 CST 2024 armv7l GNU/Linux
```

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
user@M5Core135:/home/share$ sudo ./frame_buffer_opencv
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

CoreMP135 で、アプリケーションfbi からDisplayPortとLCDにカラーバーを表示と、色がずれる。 
<img width="640" alt="S__80977923" src="https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV/assets/27625496/78c63160-3e39-43e0-bf4f-8327f33d26bf">

```
$user@M5Core135 $ apt install fbi
$user@M5Core135 $ sudo fbi -d /dev/fb0 -T 1 -a 06b.jpg
$user@M5Core135 $ sudo fbi -d /dev/fb1 -T 1 -a 06b.jpg
```

### Apendix

https://x.com/nnn112358/status/1795632180200432036


