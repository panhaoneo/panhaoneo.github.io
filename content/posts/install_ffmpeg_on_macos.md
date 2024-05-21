+++
title = 'macos编译安装ffmpeg'
date = 2023-10-20T14:40:46+08:00
draft = false
+++

```
#brew 安装依赖项
brew update
brew install automake cmake frei0r git libass libtool libvorbis libvpx opus sdl2 theora x264 x265 yasm

#编译选项
# ffmpeg 4.4
sudo ./configure --prefix=/usr/local/ \
--enable-gpl \
--enable-nonfree \
--enable-postproc \
--enable-libass \
--enable-libfdk-aac \
--enable-libfreetype \
--enable-libopenjpeg \
--enable-openssl \
--enable-libopus \
--enable-libspeex \
--enable-libvorbis \
--enable-libvpx \
--enable-libx264 \
--enable-librtmp \
--enable-pthreads \
--disable-static \
--enable-shared

make -j8 && sudo make install
```


