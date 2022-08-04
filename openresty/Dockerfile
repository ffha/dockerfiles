FROM alpine:3.15
RUN apk add --no-cache wget
WORKDIR /root
RUN wget 'http://openresty.org/package/admin@openresty.com-5ea678a6.rsa.pub'
RUN mv 'admin@openresty.com-5ea678a6.rsa.pub' /etc/apk/keys/
RUN echo "http://openresty.org/package/alpine/v3.15/main" \
    | sudo tee -a /etc/apk/repositories
RUN apk add --no-cache openresty openresty-resty
