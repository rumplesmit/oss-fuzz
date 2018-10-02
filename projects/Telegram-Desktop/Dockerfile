FROM ubuntu:16.04
MAINTAINER felipe.limaventura@gmail.com

RUN apt-get update && apt-get upgrade -y && apt-get install -y gcc-5-base libgcc-5-dev g++ libstdc++-5-dev
RUN apt-get install git libexif-dev liblzma-dev libz-dev libssl-dev libappindicator-dev libunity-dev libicu-dev libdee-dev libdrm-dev dh-autoreconf autoconf automake build-essential libass-dev libfreetype6-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-image0-dev libxcb-shm0-dev libxcb-xfixes0-dev libxcb-keysyms1-dev libxcb-icccm4-dev libxcb-render-util0-dev libxcb-util0-dev libxrender-dev libasound-dev libpulse-dev libxcb-sync0-dev libxcb-randr0-dev libx11-xcb-dev libffi-dev libncurses5-dev pkg-config texi2html zlib1g-dev yasm cmake xutils-dev bison python-xcbgen -y


#RUN apt-get install -y software-properties-common
#RUN add-apt-repository ppa:ubuntu-toolchain-r/test
#RUN add-apt-repository ppa:george-edison55/cmake-3.x
#RUN apt-get update && apt-get install -y gcc-8 g++-8 cmake
#RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60
#RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 60
#RUN add-apt-repository --remove ppa:ubuntu-toolchain-r/test -y
#RUN add-apt-repository --remove ppa:george-edison55/cmake-3.x -y


RUN MAKE_THREADS_CNT=-j8

RUN mkdir Telegram
WORKDIR Telegram

RUN git clone --recursive https://github.com/telegramdesktop/tdesktop.git

RUN mkdir Libraries
WORKDIR Libraries

RUN git clone https://github.com/ericniebler/range-v3

RUN git clone https://github.com/telegramdesktop/zlib.git
WORKDIR zlib
RUN ./configure
RUN make $MAKE_THREADS_CNT
WORKDIR ..

RUN git clone https://github.com/xiph/opus
WORKDIR opus
RUN git checkout v1.2.1
RUN ./autogen.sh
RUN ./configure
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone https://github.com/01org/libva.git
WORKDIR libva
RUN ./autogen.sh --enable-static
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone git://anongit.freedesktop.org/vdpau/libvdpau
WORKDIR libvdpau
RUN ./autogen.sh --enable-static
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone https://github.com/FFmpeg/FFmpeg.git ffmpeg
WORKDIR ffmpeg
RUN git checkout release/3.4

RUN ./configure --prefix=/usr/local --disable-programs --disable-doc --disable-everything --enable-protocol=file --enable-libopus --enable-decoder=aac --enable-decoder=aac_latm --enable-decoder=aasc --enable-decoder=flac --enable-decoder=gif --enable-decoder=h264 --enable-decoder=h264_vdpau --enable-decoder=mp1 --enable-decoder=mp1float --enable-decoder=mp2 --enable-decoder=mp2float --enable-decoder=mp3 --enable-decoder=mp3adu --enable-decoder=mp3adufloat --enable-decoder=mp3float --enable-decoder=mp3on4 --enable-decoder=mp3on4float --enable-decoder=mpeg4 --enable-decoder=mpeg4_vdpau --enable-decoder=msmpeg4v2 --enable-decoder=msmpeg4v3 --enable-decoder=opus --enable-decoder=pcm_alaw --enable-decoder=pcm_alaw_at --enable-decoder=pcm_f32be --enable-decoder=pcm_f32le --enable-decoder=pcm_f64be --enable-decoder=pcm_f64le --enable-decoder=pcm_lxf --enable-decoder=pcm_mulaw --enable-decoder=pcm_mulaw_at --enable-decoder=pcm_s16be --enable-decoder=pcm_s16be_planar --enable-decoder=pcm_s16le --enable-decoder=pcm_s16le_planar --enable-decoder=pcm_s24be --enable-decoder=pcm_s24daud --enable-decoder=pcm_s24le --enable-decoder=pcm_s24le_planar --enable-decoder=pcm_s32be --enable-decoder=pcm_s32le --enable-decoder=pcm_s32le_planar --enable-decoder=pcm_s64be --enable-decoder=pcm_s64le --enable-decoder=pcm_s8 --enable-decoder=pcm_s8_planar --enable-decoder=pcm_u16be --enable-decoder=pcm_u16le --enable-decoder=pcm_u24be --enable-decoder=pcm_u24le --enable-decoder=pcm_u32be --enable-decoder=pcm_u32le --enable-decoder=pcm_u8 --enable-decoder=pcm_zork --enable-decoder=vorbis --enable-decoder=wavpack --enable-decoder=wmalossless --enable-decoder=wmapro --enable-decoder=wmav1 --enable-decoder=wmav2 --enable-decoder=wmavoice --enable-encoder=libopus --enable-hwaccel=h264_vaapi --enable-hwaccel=h264_vdpau --enable-hwaccel=mpeg4_vaapi --enable-hwaccel=mpeg4_vdpau --enable-parser=aac --enable-parser=aac_latm --enable-parser=flac --enable-parser=h264 --enable-parser=mpeg4video --enable-parser=mpegaudio --enable-parser=opus --enable-parser=vorbis --enable-demuxer=aac --enable-demuxer=flac --enable-demuxer=gif --enable-demuxer=h264 --enable-demuxer=mov --enable-demuxer=mp3 --enable-demuxer=ogg --enable-demuxer=wav --enable-muxer=ogg --enable-muxer=opus

RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone https://git.assembla.com/portaudio.git
WORKDIR portaudio
RUN git checkout 396fe4b669
RUN ./configure
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone git://repo.or.cz/openal-soft.git
WORKDIR openal-soft
RUN git checkout v1.18
WORKDIR build
RUN cmake -D LIBTYPE:STRING=STATIC ..
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ../..

RUN git clone https://github.com/openssl/openssl
WORKDIR openssl
RUN git checkout OpenSSL_1_0_1-stable
RUN ./config
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone https://github.com/xkbcommon/libxkbcommon.git
WORKDIR libxkbcommon
RUN ./autogen.sh --disable-x11
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone git://code.qt.io/qt/qt5.git qt5_6_2
WORKDIR qt5_6_2
RUN perl init-repository --module-subset=qtbase,qtimageformats
RUN git checkout v5.6.2
WORKDIR qtimageformats
RUN git checkout v5.6.2
WORKDIR ..
WORKDIR qtbase
RUN git checkout v5.6.2
WORKDIR ..
WORKDIR qtbase
RUN git apply ../../../tdesktop/Telegram/Patches/qtbase_5_6_2.diff
WORKDIR ..
WORKDIR qtbase/src/plugins/platforminputcontexts
RUN git clone https://github.com/telegramdesktop/fcitx.git
RUN git clone https://github.com/telegramdesktop/hime.git
WORKDIR ../../../..

RUN ./configure -prefix "/usr/local/tdesktop/Qt-5.6.2" -release -force-debug-info -opensource -confirm-license -qt-zlib -qt-libpng -qt-libjpeg -qt-freetype -qt-harfbuzz -qt-pcre -qt-xcb -qt-xkbcommon-x11 -no-opengl -no-gtkstyle -static -openssl-linked -nomake examples -nomake tests

RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR ..

RUN git clone https://chromium.googlesource.com/external/gyp
WORKDIR gyp
RUN git checkout 702ac58e47
RUN git apply ../../tdesktop/Telegram/Patches/gyp.diff
WORKDIR ..

RUN git clone https://chromium.googlesource.com/breakpad/breakpad
WORKDIR breakpad
RUN git checkout bc8fb886
RUN git clone https://chromium.googlesource.com/linux-syscall-support src/third_party/lss
WORKDIR src/third_party/lss
RUN git checkout a91633d1
WORKDIR ../../..
RUN ./configure
RUN make $MAKE_THREADS_CNT
RUN make install
WORKDIR src/tools
RUN ../../../gyp/gyp  --depth=. --generator-output=.. -Goutput_dir=../out tools.gyp --format=cmake
WORKDIR ../..
WORKDIR out/Default


#RUN gcc -v
#RUN cmake --version

RUN git clone https://github.com/google/googletest.git
WORKDIR googletest/googlemock
RUN cmake CMakeLists.txt
RUN export CXX_FLAGS=-std=c++11
RUN make 

RUN cmake .
#RUN make $MAKE_THREADS_CNT dump_syms
#WORKDIR ../../..
#
#FROM gcr.io/oss-fuzz-base/base-builder
#
#WORKDIR ..
#WORKDIR tdesktop/Telegram
#RUN gyp/refresh.sh
#
#WORKDIR ..
#WORKDIR out/Release
#RUN make $MAKE_THREADS_CNT 
#
#COPY build.sh fuzzer.cc $SRC/
