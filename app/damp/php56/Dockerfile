FROM php:5.6.36-fpm

# 修复：更新源为归档仓库并处理密钥问题
RUN sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
    sed -i 's|security.debian.org|archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    echo "deb http://archive.debian.org/debian stretch contrib main" > /etc/apt/sources.list && \
    echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list

# 修复：添加缺失的目录
RUN mkdir -p /usr/share/man/man1 && \
    mkdir -p /usr/share/man/man7

# 修复：允许安装未经验证的包
RUN apt-get update && apt-get install -y --allow-unauthenticated \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libzip-dev \
        zlib1g-dev \
        libwebp-dev \
        default-libmysqlclient-dev \
        libicu-dev \
        libxml2-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) \
        mysqli \
        pdo_mysql \
        bcmath \
        zip \
        gd \
        mcrypt \
        intl \
        pcntl \
        shmop \
        sockets \
        soap \
        opcache \
    && pecl install redis-3.1.6 \
    && docker-php-ext-enable redis \
    && rm -rf /var/lib/apt/lists/*