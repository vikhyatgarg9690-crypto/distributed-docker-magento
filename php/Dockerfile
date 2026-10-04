FROM php:8.4-fpm

ARG UID=1000
ARG GID=1000

RUN groupadd -g ${GID} magento \
    && useradd -u ${UID} -g ${GID} -m -s /bin/bash magento

RUN chmod 677 /var/www

RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    unzip \
    zip \
    vim \
    cron \
    procps \
    htop \
    libzip-dev \
    libicu-dev \
    libxml2-dev \
    libxslt1-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libonig-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libreadline-dev \
    libsodium-dev \
    libmagickwand-dev \
    default-mysql-client

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg

RUN docker-php-ext-install \
    bcmath \
    ctype \
    curl \
    dom \
    fileinfo \
    gd \
    iconv \
    intl \
    mbstring \
    mysqli \
    opcache \
    pcntl \
    pdo_mysql \
    simplexml \
    soap \
    sockets \
    xsl \
    zip

RUN pecl install redis imagick \
    && docker-php-ext-enable redis imagick

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
