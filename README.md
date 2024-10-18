# ffmpeg-OpenGLTransitionEffect
An OpenGLTransition fx lib integrated to ffmpeg. The project Base on FFmpeg Version 7.1. Just apply code patch to ffmpeg 7.1 branch unsing git tools.  Then build ffmpeg to roll out your ffmpeg excuetable  program.

# Applay patch
Download repository diff patch to apply for ffmpeg soruce.

# build ffmpeg

## windows mingw64 build guide
>1.Preconditions, install tools：
```shell
pacman -S make
pacman -S diffutils
pacman -S yasm
pacman -S mingw-w64-x86_64-gcc
pacman -S mingw-w64-i686-gcc
 ```
 
>2.Install dependence libs:

```shell
pacman -Syu   # update pacman package list database
pacman -Su    # update installed package
pacman -S mingw-w64-x86_64-libass --noconfirm  # install libass
pacman -S mingw-w64-x86_64-lame --noconfirm
pacman -S mingw-w64-x86_64-fdk-aac --noconfirm
pacman -S mingw-w64-x86_64-libtheora --noconfirm
pacman -S mingw-w64-x86_64-libvpx --noconfirm
pacman -S mingw-w64-x86_64-x265 --noconfirm
pacman -S mingw-w64-x86_64-x264 --noconfirm
pacman -S mingw-w64-x86_64-opus --noconfirm
pacman -S mingw-w64-x86_64-vorbis --noconfirm
pacman -S mingw-w64-x86_64-mesa --noconfirm
pacman -S mingw-w64-x86_64-freeglut --noconfirm
```
extra libs:
- GLEW(G)
- EGL or GLFW 


>3.Then on ffmpeg path, run cofigure command
```shell
 ./configure --prefix=/usr/local  --enable-gpl --enable-nonfree --enable-libass   --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libtheora   --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265   --enable-libopus --enable-libxvid   --enable-opengl --enable-filter=gltransition --extra-libs='-lglew32s.lib -llibglfw3.a' --enable-cross-compile --arch=x86_64 --target-os=mingw64 --cross-prefix=mingw-w64-i686-
```
>4.make the program
```shell
  make
  sudo make install
```



>## Linux (ubuntu) build guide

>1.install depences:

OpenGL depences and build-essential libs
```shell
sudo apt-get install build-essential
sudo apt-get install libgl1-mesa-dev
sudo apt-get install libglu1-mesa-dev
```

Other libs used on configrue command.
```shell
sudo apt install libglu1-mesa-dev freeglut3-dev mesa-common-dev #GLU
sudo apt install libxvidcore-dev
sudo apt install libvpx-dev
sudo apt install libass-dev
sudo apt install libmp3lame-dev
sudo apt install libx265-dev
sudo apt install libx264-dev
sudo add-apt-repository ppa:jonathonf/ffmpeg-4
sudo apt update
sudo apt install libfdk-aac-dev
sudo apt install libopus-dev
sudo apt install libvorbis-dev
```
>2. run configure command

 - Use exra libs : [GLEW](http://glew.sourceforge.net/) , [glfw](http://www.glfw.org/). (--extra-libs='-lGLEW -lglfw' )
```shell
 ./configure --prefix=/usr/local --enable-gpl --enable-nonfree --enable-libass   --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libtheora   --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265   --enable-libopus --enable-libxvid   --enable-opengl --enable-filter=gltransition --extra-libs='-lGLEW -lglfw' --enable-cross-compile --enable-sdl2
 ```
 - Or use extra libs: [GLEW](http://glew.sourceforge.net/) , EGL.  (--extra-libs='-lGLEW -lEGL')
 ```shell
   ./configure --prefix=/usr/local --enable-gpl --enable-nonfree --enable-libass   --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libtheora   --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265   --enable-libopus --enable-libxvid   --enable-opengl --enable-filter=gltransition --extra-libs='-lGLEW -lEGL' --enable-cross-compile --enable-sdl2 
```
>3. make the program
```shell
  make
  sudo make install
```

# Usage of transition effect of video

Assume that you have tow input file named: v1.mp4 v2.mp4 ,then output file is out.mp4
```shell
ffmpeg -i v1.mp4 -i v2.mp4 -filter_complex "gltransition=duration=3:offset=1:source=GlitchMemories.glsl" -y out.mp4
```
Available args are : *duration* , *offset* , *source*

- duration : means transition times.
- offest : means how start transition effect delay offset times.
- source : means use the GLSL（openGL shader language）shader effect file. 

Download and use other GLSL effects,you can find here [gl-transition](https://gl-transitions.com/gallery?page=6).

# Reffercen project
- Thanks to [transitive-bullshit/ffmpeg-gl-transition](https://github.com/transitive-bullshit/ffmpeg-gl-transition) on github repository.
- [ffmpeg](https://github.com/FFmpeg/FFmpeg)
- [GLEW](http://glew.sourceforge.net/) 
- [glfw](http://www.glfw.org/)


