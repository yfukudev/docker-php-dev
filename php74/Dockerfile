FROM php:7.4-fpm-alpine3.13

RUN apk add --update --no-cache tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    echo "Asia/Tokyo" > /etc/timezone && \
    apk del tzdata 

RUN apk add --update --no-cache \
    curl-dev \
    libxml2-dev \
    postgresql-dev \
    freetype-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    zip \
    libzip-dev \
    unzip \
    gmp-dev \
    oniguruma-dev \
    autoconf \
    gcc \
    g++ \
    make \
    npm

RUN docker-php-source extract \
    && cp /usr/src/php/ext/openssl/config0.m4 /usr/src/php/ext/openssl/config.m4 \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install pdo \
    pdo_mysql \
    mysqli \
    pdo_pgsql \
    pgsql \
    mbstring \
    bcmath \
    curl \
    ctype \
    fileinfo \
    xml \
    json \
    openssl \
    gd \
    zip \
    gmp \
    tokenizer \
    opcache

RUN curl -sSL https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 -o mhsendmail \
    && chmod +x mhsendmail \
    && mv mhsendmail /usr/local/bin/mhsendmail

COPY ./php.ini /usr/local/etc/php/php.ini

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer