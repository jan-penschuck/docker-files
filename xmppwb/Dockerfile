FROM        python:alpine
MAINTAINER  sneak@gruppenrat.net

RUN apk add --no-cache make gcc musl-dev

RUN         pip install --upgrade xmppwb

VOLUME      /etc/xmppwb

ENTRYPOINT  ["xmppwb","--config","/etc/xmppwb/xmppwb.conf"]
