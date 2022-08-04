FROM php:8.1-fpm-alpine
RUN mkdir /app
WORKDIR /app
RUN apk add wget unzip nginx nginx-mod-http-brotli tini
ARG TYPECHO_VERSION 1.2.0
RUN wget https://github.com/typecho/typecho/releases/download/${TYPECHO_VERSION}/typecho.zip
RUN unzip typecho.zip
COPY nginx.conf /etc/nginx/http.d/server.conf
COPY start.sh /start.sh
RUN chmod 755 /start.sh
ENTRYPOINT ["/sbin/tini", "--"]
CMD /start.sh
