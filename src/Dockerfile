FROM alpine:3.4

MAINTAINER takafumiotake<tikutaka.dev@gmail.com>

COPY runit_bootstrap /usr/sbin/runit_bootstrap

RUN RUNIT_VERSION="2.1.2" \
    && RUNIT_SHA1="398f7bf995acd58797c1d4a7bcd75cc1fc83aa66" \
    && apk add --no-cache --virtual .build-deps \
        curl \
        tar \
        make \
        gcc \
        musl-dev \
    && curl -fSL http://smarden.org/runit/runit-$RUNIT_VERSION.tar.gz -o runit.tar.gz \
    && echo "$RUNIT_SHA1  runit.tar.gz" | sha1sum -c \
    && mkdir -p /usr/src \
    && tar -zxC /usr/src -f runit.tar.gz --strip-component=2 \
    && rm -f runit.tar.gz \
    && cd /usr/src/runit/src \
    && make \
    && cat package/commands | xargs -I {} mv -f src/{} /sbin/ \
    && cd / \
    && rm -rf /usr/src/runit \
    && apk del .build-deps \
    && mkdir /service
    && chmod 755 /usr/sbin/runit_bootstrap

ENTRYPOINT ["/usr/sbin/runit_bootstrap"]
