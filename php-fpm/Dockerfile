FROM php:fpm

RUN apt-get update

# Install mcrypt
RUN apt-get install -y \
        libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) mcrypt

# Install intl
RUN apt-get install -y \
        libicu-dev \
    && docker-php-ext-install -j$(nproc) intl

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
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \ 
    && docker-php-ext-install -j$(nproc) ldap

# Install postgres
RUN apt-get install -y \
        libpq-dev \
    && docker-php-ext-install -j$(nproc) pdo_pgsql pgsql

# Install mysql
RUN docker-php-ext-install -j$(nproc) mysqli pdo_mysql

# Install opcache      
RUN docker-php-ext-install -j$(nproc) opcache

# Install zip
RUN docker-php-ext-install -j$(nproc) zip

# Install bcmath
RUN docker-php-ext-install -j$(nproc) bcmath

# Install bz2
RUN apt-get install -y \
        libbz2-dev \
    && docker-php-ext-install -j$(nproc) bz2

# Install calendar
RUN docker-php-ext-install -j$(nproc) calendar

# Install curl
RUN apt-get install -y \
        libcurl4-openssl-dev \
    && docker-php-ext-install -j$(nproc) curl

# Install exif
RUN docker-php-ext-install -j$(nproc) exif

# Install json
RUN docker-php-ext-install -j$(nproc) json

# Install xml
RUN apt-get install -y \
        libxml2-dev \
        libxslt1-dev \
    && docker-php-ext-install -j$(nproc) xml xmlrpc xsl

# Install pspell
RUN apt-get install -y \
        libpspell-dev \
    && docker-php-ext-install -j$(nproc) pspell

# Install readline
RUN apt-get install -y \
        libedit-dev \
    && docker-php-ext-install -j$(nproc) readline

# Install fileinfo
RUN docker-php-ext-install -j$(nproc) fileinfo

# Install enchant
RUN apt-get install -y \
        libenchant-dev \
    && docker-php-ext-install -j$(nproc) enchant

# Install pcntl
RUN docker-php-ext-install -j$(nproc) pcntl

# Install tidy
RUN apt-get install -y \
        libtidy-dev \
    && docker-php-ext-install -j$(nproc) tidy

RUN apt-get install -y \
        cron nano

ADD run.sh /usr/local/bin/
