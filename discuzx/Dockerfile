FROM php:8.1-fpm-alpine
WORKDIR /usr/src
RUN apk add wget unzip nginx nginx-mod-http-brotli tini
ARG DISCUZX_VERSION 20220518
RUN wget https://www.discuz.net/down/Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip
RUN unzip Discuz_X3.4_SC_UTF8_${DISCUZX_VERSION}.zip
WORKDIR /usr/src/upload
RUN mkdir /app
COPY nginx.conf /etc/nginx/http.d/server.conf
COPY start.sh /start.sh
RUN chmod 755 /start.sh
RUN cp -r ./ /app
ENTRYPOINT ["/sbin/tini", "--"]
CMD /start.sh
