ARG IMAGE_TAG=7.4-fpm-alpine3.11
FROM php:${IMAGE_TAG}

ARG IMAGE_TAG

RUN set -xe && \
    apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/v3.11/main/ \
      icu \
      glib \
      libxrender \
      libxext \
      fontconfig \
      libpng \
      libjpeg-turbo \
      libssl1.1 \
      libcrypto1.1 && \
    apk add --no-cache --virtual .build-deps \
      $PHPIZE_DEPS \
      zlib-dev \
      icu-dev \
      libpng-dev \
      libjpeg-turbo-dev \
      oniguruma-dev && \
    pecl install apcu-5.1.18 && \
    pecl install apcu_bc-1.0.5 && \
    docker-php-ext-configure \
      intl && \
    if [ "$IMAGE_TAG" = "7.4-fpm-alpine3.11" ]; then \
      docker-php-ext-configure gd --with-jpeg=/usr/include/; \
    else \
      docker-php-ext-configure gd --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
    fi && \
    docker-php-ext-install \
      pdo_mysql \
      intl \
      gd && \
    docker-php-ext-enable apcu && \
    docker-php-ext-enable apc && \
    apk del .build-deps && \
    rm -rf /tmp/* /usr/local/lib/php/doc/* /var/cache/apk/*
