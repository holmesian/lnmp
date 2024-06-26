FROM php:8.2-fpm

LABEL maintainer="Holmesian <i@holmesian.org>"

#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# WORKDIR /www
#COPY . .
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/

# 国内网络增加下列
# RUN sed -i "s@http://deb.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list \
#     && sed -i "s@http://security.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list

#  更新安装依赖包和PHP核心拓展 remove zlibc
RUN apt-get update  \
    && apt-get install -y --no-install-recommends git libbz2-dev libmagickwand-dev libmcrypt-dev zlib1g-dev  libzip-dev libfreetype6-dev libjpeg62-turbo-dev libwebp-dev libjpeg-dev libpng-dev \
    && cd /usr/local/bin/ \
    && apt-get upgrade -y \
    && docker-php-source extract \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) gd bcmath zip pdo_mysql opcache mysqli \
    && docker-php-ext-enable gd  \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -r /var/lib/apt/lists/*

# Donwload and install composer
RUN curl -sSL "https://getcomposer.org/installer" | php \
        && chmod +x composer.phar \
                && mv composer.phar /usr/local/bin/composer \
        && composer config -g repo.packagist composer https://packagist.phpcomposer.com

WORKDIR /www
RUN usermod -u 1000 www-data