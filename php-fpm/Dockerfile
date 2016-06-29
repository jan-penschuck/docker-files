FROM php:fpm

MAINTAINER sneak

RUN apt-get update

# Install mongodb
RUN apt-get install -y \
        libssl-dev \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb

# Install gd
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Install redis
ENV PHPREDIS_VERSION=php7
RUN cd /usr/src/php/ext \
    && curl -q https://codeload.github.com/phpredis/phpredis/tar.gz/$PHPREDIS_VERSION | tar -xz \
    && docker-php-ext-install phpredis-$PHPREDIS_VERSION

# Install ldap
RUN apt-get install -y \
        libldap2-dev \
        libpq-dev \
        libbz2-dev \
        libcurl4-openssl-dev \
        libxml2-dev \
        libxslt1-dev \
        libpspell-dev \
        libedit-dev \
        libenchant-dev \
        libtidy-dev \
        libmcrypt-dev \
        libicu-dev \
        libc-client2007e-dev \
        libkrb5-dev

RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \ 
    && docker-php-ext-install -j$(nproc) ldap

RUN docker-php-ext-install -j$(nproc) pdo_pgsql \
        pgsql \
        mysqli \
        pdo_mysql \
        opcache \
        zip \
        bcmath \
        bz2 \
        calendar \
        curl \
        exif \
        json \
        xml \
        xmlrpc \
        xsl \
        pspell \
        readline \
        mcrypt \
        intl \
        fileinfo \
        enchant \
        pcntl \
        tidy \
        gettext \
        imap \
        iconv \
        dom \
        session \
        ctype \
        phar \
        mbstring

RUN apt-get install -y \
        cron vim sudo

ADD php-fpm/run.sh /usr/local/bin/

WORKDIR /srv
