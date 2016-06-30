FROM alpine:edge

MAINTAINER sneak

RUN apk update \
    && apk upgrade
RUN apk add --no-cache git curl ca-certificates bash tini \
    && update-ca-certificates \
    && apk add --no-cache --virtual .build_tools wget tar \
    && wget -qO- https://getcaddy.com \
      | bash -s cors,git,hugo,ipfilter,jsonp,jwt,mailout,prometheus,realip,search,upload \
    && apk del --purge .build_tools \
    && rm -rf \
      /usr/share/doc \
      /usr/share/man \
      /tmp/* \
      /var/cache/apk/* 

VOLUME ["/srv", "/root/.caddy"]

EXPOSE 80 443

ENTRYPOINT ["tini"]

CMD ["caddy", "--conf", "/etc/Caddyfile"]
