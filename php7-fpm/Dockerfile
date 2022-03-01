FROM php:7.4-fpm

LABEL maintainer="Holmesian <i@holmesian.org>"


#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone 
# 国内网络增加下列
RUN sed -i "s@http://deb.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && sed -i "s@http://security.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list

# WORKDIR /www
#COPY . .
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/

#  更新安装依赖包和PHP核心拓展 remove zlibc
RUN apt-get update  \
    && apt-get install -y --no-install-recommends git libbz2-dev libmagickwand-dev libmcrypt-dev zlib1g-dev  libzip-dev libfreetype6-dev libjpeg62-turbo-dev\
    && docker-php-ext-install -j$(nproc) gd bcmath zip pdo_mysql opcache mysqli\
    && pecl install imagick mcrypt-1.0.3 redis-5.1.1 \
    && docker-php-ext-enable imagick mcrypt  redis \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure opcache --enable-opcache \
    && apt-get upgrade -y \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -r /var/lib/apt/lists/*
        

# Donwload and install composer
RUN curl -sSL "https://getcomposer.org/installer" | php \
        && chmod +x composer.phar \
		&& mv composer.phar /usr/local/bin/composer \
        && composer config -g repo.packagist composer https://packagist.phpcomposer.com 

WORKDIR /www
RUN usermod -u 1000 www-data
