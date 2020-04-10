FROM php:5.6-fpm
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
        && docker-php-ext-install mcrypt \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && pecl install xdebug-2.5.5  imagick-beta\
        && docker-php-ext-enable xdebug imagick mcrypt \
        && docker-php-ext-configure opcache --enable-opcache \
        && rm -r /var/lib/apt/lists/*
        

WORKDIR /www
RUN usermod -u 1000 www-data
