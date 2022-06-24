ARG ARCH=

FROM ${ARCH}alpine:latest as builder

LABEL maintainer="laj1z"

RUN apk update && apk add make gcc git g++ libc-dev bash util-linux-dev

WORKDIR /tmp
RUN git clone https://github.com/laj1z/xupnpd-s \
    && cd xupnpd-s/src \
    && make

FROM ${ARCH}alpine:latest

WORKDIR /xupnpd
COPY --from=builder /tmp/xupnpd-s/src/xupnpd-x86 ./xupnpd-x86
COPY --from=builder /tmp/xupnpd-s/lua/. ./

RUN mkdir playlists
VOLUME /xupnpd/playlists

ENTRYPOINT ["/xupnpd/xupnpd-x86"]
