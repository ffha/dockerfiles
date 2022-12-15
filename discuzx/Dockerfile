FROM php:8.1-fpm-alpine
WORKDIR /usr/src
RUN apk add wget unzip nginx nginx-mod-http-brotli tini
ARG DISCUZX_VERSION 20220518
RUN apk add wget --no-cache unzip nginx nginx-mod-http-brotli tini && wget https://www.discuz.net/down/Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip && unzip Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip
WORKDIR /usr/src/upload
COPY nginx.conf /etc/nginx/http.d/server.conf
COPY start.sh /start.sh
RUN mkdir /app && chmod 755 /start.sh && cp -r ./ /app && cd / && rm -rf /usr/src
ENTRYPOINT ["/sbin/tini", "--"]
CMD /start.sh
