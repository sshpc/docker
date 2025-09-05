FROM php:7.4.33-fpm

# 修复：更新源为 bullseye 主仓库（移除安全仓库）
RUN sed -i '/security/d' /etc/apt/sources.list && \
    sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
    sed -i 's/bullseye-updates/bullseye/g' /etc/apt/sources.list

# 安装系统依赖
RUN apt-get update && apt-get install -y --allow-unauthenticated \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
        zlib1g-dev \
        libonig-dev \
        libwebp-dev \
        default-libmysqlclient-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) \
        mysqli \
        pdo_mysql \
        bcmath \
        zip \
        gd \
    && pecl install redis-5.3.7 \
    && docker-php-ext-enable redis

# 单独安装mcrypt
RUN apt-get install -y --allow-unauthenticated libmcrypt-dev \
    && pecl install mcrypt-1.0.5 \
    && docker-php-ext-enable mcrypt