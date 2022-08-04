FROM alpine:edge
RUN apk add --no-cache tini musl-dev gcc make curl zlib-dev perl perl-dev pcre-dev linux-headers brotli-dev git
WORKDIR /usr/src
RUN git clone https://github.com/google/ngx_brotli.git
RUN curl -sO https://tengine.taobao.org/download/tengine-2.3.3.tar.gz
RUN curl -sO https://www.openssl.org/source/openssl-1.1.1q.tar.gz
RUN tar xzf openssl-1.1.1q.tar.gz && tar xzf tengine-2.3.3.tar.gz
WORKDIR /usr/src/tengine-2.3.3
RUN addgroup -g 101 -S nginx && adduser -S -D -H -u 101 -h /var/log/nginx -s /sbin/nologin -G nginx -g nginx nginx
RUN ./configure --with-compat --with-http_perl_module --with-stream_sni --add-module=/usr/src/ngx_brotli --prefix=/usr/share/nginx --user=nginx --group=nginx --sbin-path=/sbin/nginx --modules-path=/usr/lib/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --pid-path=/run/nginx.pid --lock-path=/run/nginx.lock --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --http-log-path=/var/log/nginx/access.log --http-client-body-temp-path=/tmp/client_tmp --http-proxy-temp-path=/tmp/proxy_tmp --http-fastcgi-temp-path=/tmp/fcgi_tmp --http-uwsgi-temp-path=/tmp/uwsgi_tmp --http-scgi-temp-path=/tmp/scgi_tmp --with-stream --with-stream_ssl_module --with-stream_realip_module --with-openssl=/usr/src/openssl-1.1.1q
RUN make -j $(nproc) && make install
WORKDIR /
RUN apk del musl-dev gcc make curl zlib-dev brotli-dev pcre-dev perl-dev linux-headers git && apk add --no-cache brotli-libs pcre
RUN rm -rf /usr/src
RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
ENTRYPOINT ["/sbin/tini", "--"]
EXPOSE 80
STOPSIGNAL SIGQUIT
CMD nginx -g "daemon off;"
