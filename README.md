# CoreMP135_framebuffer_OpenCV

CoreMP135で、LCDとDisplayPort(HDMI)に画像を表示するサンプルです。ライブラリにはOpenCV-Mobileを使っています。  
CoreMP135では、画像データをframebufferに書き込む前に、以下の色変換が必要です。(Fimware ver:M5_CoreMP135_debian12_20240515)
~~DisplayPortとLCDとで、BチャンネルとRチャンネルを逆にする必要があります。~~

This is a sample that displays images on LCD and DisplayPort using coremp135. I am using OpenCV-Mobile as the library.  
In CoreMP135, the color conversion written to framebuffer is different. ~~The B and R channels must be reversed between DisplayPort and LCD.~~

2024/5/30以降のlt8618sxb_mcu_configを導入することで、DisplayPortとLCDとで同じ色変換となる。  
By running lt8618sxb_mcu_config after 2024/5/30, the color conversion will be the same for DisplayPort and LCD.  
https://github.com/m5stack/CoreMP135_buildroot-external-st/commit/b881954c214ccec3e6956fdbda0db5e5a4bebd0e  
https://github.com/m5stack/M5Stack_Linux_Libs/commit/e7cf5787bd4f9206ec88721b54c44f59a6b3f72c  


|Display|Color conversion | resolution |
|-------------| ------------- | ------------- |
|DisplayPort(HDMI)| BGR888⇒BGR565   |  1280x720   |
|LCD|BGR888⇒BGR565 | 320x240    |


<img width="640" alt="S__80977923" src="https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV/assets/27625496/7253fda7-6f79-4ebc-9a60-d4bf5b55b4bf">

## M5_CoreMP135_Enviroment

The firmware is "M5_CoreMP135_debian12_20240515"  
https://docs.m5stack.com/en/guide/linux/coremp135/image ⇒ M5_CoreMP135_debian12_20240515	

```
$ $user@M5Core135 $ uname -a
Linux M5Core135 5.15.118 #1 SMP PREEMPT Tue May 7 15:14:07 CST 2024 armv7l GNU/Linux
```

### Cross Build instraction (Ubuntu22.04)

```
$ sudo apt install arm-linux-gnueabihf-g++ arm-linux-gnueabihf-gcc cmake
$ git clone https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV.git
$ cd CoreMP135_framebuffer_OpenCV
$ mkdir build
$ cd build
$ cmake ..
$ make
```

#### OpenCV-Mobile Cross Build instraction
```
$ wget -q https://github.com/nihui/opencv-mobile/releases/latest/download/opencv-mobile-4.9.0.zip
$ unzip -q opencv-mobile-4.9.0.zip
$ cd opencv-mobile-4.9.0
$ cmake -B build/arm -DCMAKE_TOOLCHAIN_FILE=./arm-gnueabihf.toolchain.cmake -DCMAKE_BUILD_TYPE=Release `cat ./options.txt` -DBUILD_opencv_world=OFF .
$ cmake --build build/arm
$ cmake --install build/arm --prefix install/arm
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

### Apendix
CoreMP135 で、アプリケーションfbi からDisplayPortとLCDにカラーバーを表示と、色がずれる問題が発生した。 
<img width="640" alt="S__80977923" src="https://github.com/nnn112358/CoreMP135_framebuffer_OpenCV/assets/27625496/78c63160-3e39-43e0-bf4f-8327f33d26bf">

2024/5/30以降のlt8618sxb_mcu_configを導入することで、DisplayPortとLCDとで同じ色変換となり解消した。  
By running lt8618sxb_mcu_config after 2024/5/30, the color conversion will be the same for DisplayPort and LCD.  

経緯はこちら。  
https://x.com/nnn112358/status/1795632180200432036  
https://x.com/dollychun/status/1796065952519409862  
https://x.com/ciniml/status/1796068254600814990  

```
$user@M5Core135 $ wget https://www.eizo.co.jp/eizolibrary/other/itmedia04/06b.jpg
$user@M5Core135 $ apt install fbi
$user@M5Core135 $ sudo fbi -d /dev/fb0 -T 1 -a 06b.jpg
$user@M5Core135 $ sudo fbi -d /dev/fb1 -T 1 -a 06b.jpg
```




