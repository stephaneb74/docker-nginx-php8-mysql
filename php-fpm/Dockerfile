FROM php:8.2.6-fpm-alpine3.18

RUN apk --update --no-cache add busybox-extras

RUN apk --no-cache add icu-dev \
    busybox-extras \
    nano \
    autoconf \
    git \
    supervisor \
    zip \
    oniguruma-dev \
    zlib-dev \
    libpng-dev \
    libzip-dev \
    curl-dev \
    openssl-dev \
    libpq-dev \
    openssl \
    openssl-dev \
    libedit \
    libedit-dev \
    libxml2-dev \
    autoconf \
    curl \
    libstdc++ \
    libssh2-dev \
    build-base \
    bash \
    libmemcached-dev

RUN apk add --no-cache --virtual .build-deps-full \
        binutils-gold \
        g++ \
        gcc \
        gnupg \
        libgcc \
        linux-headers \
        make \
        python3

RUN docker-php-ext-configure intl
RUN docker-php-ext-configure mbstring
RUN docker-php-ext-configure mysqli
RUN docker-php-ext-configure pcntl
RUN docker-php-ext-configure gd
RUN docker-php-ext-configure exif
RUN docker-php-ext-configure zip
RUN docker-php-ext-configure curl

RUN docker-php-ext-install intl \
    mbstring \
    mysqli \
    pdo \
    pdo_mysql \
    pcntl \
    gd \
    exif \
    zip \
    curl \
    xml \
    simplexml \
    bcmath \
    sockets

RUN apk add --no-cache --virtual .build-deps \
        shadow \
        g++ \
        make \
        autoconf

RUN apk add libgomp gcompat imagemagick-dev imagemagick \
    && pecl install imagick-beta \
    && pecl install igbinary \
    && pecl install memcached \
    && pecl install msgpack \
    && docker-php-ext-enable imagick \
    && apk del .build-deps

RUN pecl install raphf && \
    docker-php-ext-enable raphf && \
    pecl install pecl_http && \
    echo "extension=http" >> /usr/local/etc/php/conf.d/docker-php-ext-raphf.ini

COPY docker-php-entrypoint /usr/local/bin
COPY php.ini /usr/local/etc/php

WORKDIR /usr/local/etc/php-fpm.d
# COPY conf.d/www.conf .

EXPOSE 9001
CMD ["php-fpm"]
