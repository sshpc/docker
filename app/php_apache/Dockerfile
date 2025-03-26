# 使用 PHP  和 Apache 的基础镜像
#FROM php:7.4.33-apache
FROM php:5.6.36-apache
#FROM php:5.5.38-apache

# 移除stretch-updates相关的源配置行，避免更新时出现问题
RUN sed -i '/stretch-updates/d' /etc/apt/sources.list

# 替换Debian stretch的源为存档库源
RUN sed -i 's/deb.debian.org\/debian/archive.debian.org\/debian/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org\/debian-security/archive.debian.org\/debian-security/g' /etc/apt/sources.list

RUN apt update && apt install -y libmhash-dev libmcrypt-dev libwebp-dev libjpeg-dev libpng-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include --with-png-dir=/usr/include --with-webp-dir=/usr/include 
# 安装必要的 PHP 扩展
RUN docker-php-ext-install mysqli pdo pdo_mysql mcrypt bcmath gd zip


# 安装redis
#RUN pecl install -y redis
#RUN docker-php-ext-enable redis

# 启用 Apache 模块
RUN a2enmod rewrite

# 设置工作目录
WORKDIR /var/www

# 复制本地的 PHP 配置文件（如果需要）
# COPY ./php.ini /usr/local/etc/php/
