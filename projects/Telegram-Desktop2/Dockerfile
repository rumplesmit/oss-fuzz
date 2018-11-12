FROM gcr.io/oss-fuzz-base/base-builder
#FROM debian:jessie
MAINTAINER felipe.limaventura@gmail.com

# Telegram Version 1.4.3

RUN apt-get update 
RUN apt-get install apt-utils -y
RUN apt-get install dbus-x11 -y
RUN apt-get install dunst -y
RUN apt-get install hunspell-en-us -y
RUN apt-get install python3-dbus -y
RUN apt-get install software-properties-common -y
RUN apt-get install libx11-xcb1 -y
RUN apt-get install  gconf2 -y
RUN apt-get install xz-utils -y
RUN apt-get install wget -y
# --no-install-recommends && \
RUN apt-get clean
# rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget https://telegram.org/dl/desktop/linux/tsetup.1.4.3.tar.xz -O /telegram.tar.xz
#cd /tmp/ && \
RUN  tar xvfJ /telegram.tar.xz
#mv /tmp/Telegram/Telegram /usr/bin/Telegram && \
#rm -rf /tmp/{telegram.tar.xz,Telegram} && \
#rm /etc/fonts/conf.d/10-scale-bitmap-fonts.conf && \
#fc-cache -fv

 ENV QT_XKB_CONFIG_ROOT=/usr/share/X11/xkb

 # Autorun Telegram
 CMD ["/usr/bin/Telegram"]

WORKDIR Telegram-Desktop2
COPY build.sh $SRC/
