FROM alpine:3.4

MAINTAINER takafumiotake<tikutaka.dev@gmail.com>

COPY runit_bootstrap /usr/sbin/runit_bootstrap

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && apk add --no-cache --update \
        runit \
    && mkdir /service \
    && chmod 755 /usr/sbin/runit_bootstrap

ENTRYPOINT ["/usr/sbin/runit_bootstrap"]
