FROM golang:alpine as builder
RUN apk add --no-cache make build-base git
WORKDIR /usr/src
RUN git clone https://github.com/goproxyio/goproxy .
RUN git checkout v2.0.7
RUN make
FROM alpine as runner
WORKDIR /app
COPY --from=builder /usr/src/bin/goproxy .
RUN apk add --no-cache tini
ENTRYPOINT ["/sbin/tini", "--"]
EXPOSE 80
CMD ["/app/goproxy", "-listen=0.0.0.0:80", "-cacheDir=/tmp"]
