FROM derjudge/archlinux:latest

MAINTAINER sneak

RUN pacman -Sy archlinux-keyring && pacman -Syyu
RUN pacman -S --noconfirm \
        dbmail \
        libsieve \
        postfix \
        cyrus-sasl \
        cyrus-sasl-ldap \
        syslog-ng \
        json-c 

RUN pacman -Scc --noconfirm
RUN useradd dbmail &&  mkdir /var/run/dbmail /var/log/dbmail && chown dbmail:dbmail /var/run/dbmail /var/log/dbmail

VOLUME /etc/postfix
VOLUME /var/spool/postfix

EXPOSE 24 25 143 587 993

CMD echo "starting servers..." \
    && syslog-ng \
    && saslauthd -a ldap \
    && postfix -c /etc/postfix start \
    && dbmail-lmtpd \
    && dbmail-timsieved \
    && dbmail-imapd -v -D
