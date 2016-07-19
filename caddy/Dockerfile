FROM alpine:edge

MAINTAINER sneak

RUN apk update \
    && apk upgrade
RUN apk add --no-cache git curl ca-certificates bash tini \
    && update-ca-certificates \
    && apk add --no-cache --virtual .build_tools wget tar \
    && curl "https://caddyserver.com/download/build?os=linux&arch=amd64&features=filemanager%2Cgit%2Chugo%2Cipfilter%2Clocale%2Cmailout%2Cminify%2Cprometheus%2Crealip%2Csearch%2Ccloudflare%2Cdigitalocean%2Cdnsimple%2Cdyn%2Cgandi%2Cgooglecloud%2Cnamecheap%2Crfc2136%2Croute53%2Cvultr" \
      | tar --no-same-owner -C /usr/bin/ -xz caddy \
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
