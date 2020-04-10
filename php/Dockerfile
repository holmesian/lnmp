FROM php:7.3.8-fpm
MAINTAINER holmesian "i@holmesian.org"

#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# WORKDIR /www
COPY . .
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/

#  更新安装依赖包和PHP核心拓展
RUN apt-get update && apt-get install -y \
        git \
        libzip-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libbz2-dev \
    && apt-get install -y --no-install-recommends libmagickwand-dev libmcrypt-dev  zlib1g-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd bcmath \
        && docker-php-ext-install zip \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install opcache \
        && docker-php-ext-install mysqli \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && pecl install xdebug-2.8.1 imagick-3.4.4 mcrypt-1.0.2 swoole-4.4.3 \
        && docker-php-ext-enable xdebug imagick mcrypt  swoole\
        && docker-php-ext-configure opcache --enable-opcache \
        && rm -r /var/lib/apt/lists/*
        

WORKDIR /www
RUN usermod -u 1000 www-data
