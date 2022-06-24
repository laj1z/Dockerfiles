ARG ARCH=

FROM ${ARCH}alpine:latest as builder

LABEL maintainer="laj1z"

RUN apk update && apk add make gcc git libc-dev openssh-client

WORKDIR /tmp
RUN git clone https://github.com/pcherenkov/udpxy.git \
    && cd udpxy/chipmunk \
    && make && make install

FROM ${ARCH}alpine:latest

COPY --from=builder /usr/local/bin/udpxy /usr/local/bin/udpxy
COPY --from=builder /usr/local/bin/udpxrec /usr/local/bin/udpxrec

ENTRYPOINT ["/usr/local/bin/udpxy"]
