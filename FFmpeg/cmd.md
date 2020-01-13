ffmpeg -i LarvaInNewYorkThemeSong.mp4 -vcodec copy -acodec copy 0.mkv
ffmpeg -i LarvaInNewYorkThemeSong.mp4 -an -vcodec copy 0.h264
ffmpeg -i LarvaInNewYorkThemeSong.mp4 -vn -acodec copy 0.aac
ffmpeg -i LarvaInNewYorkThemeSong.mp4 -an -c:v rawvideo -pix_fmt yuv420p 0.yuv
ffplay -s 1280x720 0.yuv
ffmpeg -i LarvaInNewYorkThemeSong.mp4 -vn -ar 44100 -ac 2 -f s16le 0.pcm
ffplay -ar 44100 -ac 2 -f s16le 0.pcm


ffmpeg -i LarvaInNewYorkThemeSong.mp4 -vf crop=in_w-200:in_h-200 -c:v libx264 -c:a copy 00.mp4
ffmpeg -i LarvaInNewYorkThemeSong.mp4 -ss 00:00:00 -t 10 0.mp4
ffmpeg -f concat -i inputs.txt 0000.mp4

ffmpeg -i LarvaInNewYorkThemeSong.mp4 -r 1 -f image2 image-%3d.jpeg
ffmpeg -i image-%3d.jpeg out.mp4


ffmpeg -re i LarvaInNewYorkThemeSong.mp4 -c copy -f flv rtmp://server/live
ffmpeg -i rtmp://server/live -c copy dump.flv

-movflags faststart


gcc hello_ffmpeg.c -o hello_ffmpeg -lavutil


sudo apt-get install nasm yasm
sudo apt-get install libx11-dev
sudo apt-get install xorg-dev
sudo apt-get install sdl


sudo apt-get install openssl libssl-dev
sudo apt-get install libpcre3 libpcre3-dev

sudo apt-get install zlib1g-dev

sudo apt-get install pcre pcre-devel openssl openssl-devel


sudo apt-get install build-essential libtool


https://ftp.pcre.org/pub/pcre/pcre-8.43.tar.gz
https://sourceforge.net/projects/libpng/files/zlib/1.2.11/zlib-1.2.11.tar.gz
http://zlib.net/zlib-1.2.11.tar.gz
https://www.openssl.org/source/openssl-1.1.1d.tar.gz

./configure --with-pcre=../nginx-dependence/pcre-8.43 --with-zlib=../nginx-dependence/zlib-1.2.11 --with-openssl=../nginx-dependence/openssl-1.1.1d --with-http_ssl_module --add-module=../nginx-dependence/nginx-rtmp-module-1.2.1


./configure --prefix=/usr/local/nginx --with-pcre=../nginx-dependence/pcre-8.41 --with-zlib=../nginx-dependence/zlib-1.2.11 

adb shell am start -a android.intent.action.VIEW -d http://192.168.19.192:8080/videos/10.mp4 -n 
org.videolan.vlc/.gui.video.VideoPlayerActivity
com.mxtech.videoplayer.ad/.ActivityScreen


https://sourceforge.net/projects/mingw-w64/files/
http://www.msys2.org/
http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20190524.exe

http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
https://www.nasm.us/pub/nasm/releasebuilds/


https://pkgs.org/


pkg-config --libs libavformat