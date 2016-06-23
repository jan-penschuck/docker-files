FROM debian:stretch

MAINTAINER sneak

ENV     DEBIAN_FRONTEND=noninteractive

RUN     apt-get update \
        && apt-get dist-upgrade -yq \
        && apt-get install -yq --no-install-recommends s3ql s3cmd fuse wget nano \
        && apt-get clean
RUN     mkdir /data /volume /root/.s3ql
RUN     chmod a+rwx /data /volume
COPY    s3ql/authinfo2 /root/.s3ql/authinfo2 
RUN     chmod 600 /root/.s3ql/authinfo2
RUN     cd /usr/local/bin \
        && wget -qqq https://github.com/TentativeConvert/Syndicator/raw/master/unison-binaries/unison-fsmonitor \
                     https://github.com/TentativeConvert/Syndicator/raw/master/unison-binaries/unison \
                     https://github.com/TentativeConvert/Syndicator/raw/master/unison-binaries/unison-2.48.3 \
        && chmod +x uni* && cd
RUN     export TERM=xterm
RUN     groupadd -g 1000 git
RUN     adduser --system --uid=1000 --gid=1000 --shell /bin/bash git

VOLUME  /volume

CMD     s3ql_verify s3://gruppenrat-net/data \
        && mount.s3ql --allow-root s3://gruppenrat-net/data /data \
        && /usr/local/bin/unison-2.48.3 -times -batch -auto -fastcheck=true -repeat=watch -terse /volume /data
