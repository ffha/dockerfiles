FROM php:8.1-apache
WORKDIR /usr/src
RUN apt-get install -y wget unzip
ARG DISCUZX_VERSION 20220518
RUN wget https://www.discuz.net/down/Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip
RUN unzip Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip
WORKDIR /usr/src/upload
RUN cp -r ./ /var/www/html
