FROM alpine
RUN apk add --no-cache tini musl-dev gcc make curl openssl-dev pcre2-dev zlib-dev
WORKDIR /usr/src
ARG TENGINE_VER 2.3.3
RUN curl -O "https://tengine.taobao.org/download/tengine-${TENGINE_VER}.tar.gz"
RUN tar zxvf tengine-${TENGINE_VER}.tar.gz
WORKDIR /usr/src/tengine-${TENGINE_VER}
RUN ./configure --with-compat --prefix=/usr/share/nginx --sbin-path=/sbin/nginx --modules-path=/usr/lib/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --pid-path=/run/nginx.pid --lock-path=/run/nginx.lock --with-threads --with-file-aio --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --http-log-path=/var/log/nginx/access.log --http-client-body-temp-path=/tmp/client_tmp --http-proxy-temp-path=/tmp/proxy_tmp --http-fastcgi-temp-path=/tmp/fcgi_tmp --http-uwsgi-temp-path=/tmp/uwsgi_tmp --http-scgi-temp-path=/tmp/scgi_tmp --with-stream --with-stream_ssl_module --with-stream_realip_module
RUN make -j $(nproc)
RUN make install
RUN apk del openssl-dev musl-dev gcc make curl zlib-dev
RUN apk add --no-cache zlib libssl3 libcrypto3 pcre2
ENTRYPOINT ["/sbin/tini", "--"]
EXPOSE 80
CMD nginx -g "daemon off;"

 
