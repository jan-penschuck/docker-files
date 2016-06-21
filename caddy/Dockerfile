FROM janeczku/alpine-kubernetes:latest

RUN apk update \
    && apk upgrade
RUN apk add --no-cache tini git curl ca-certificates \
    && update-ca-certificates \
    && apk add --no-cache --virtual .build_tools wget tar bash \
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

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["caddy", "--conf", "/etc/Caddyfile"]
