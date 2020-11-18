FROM php:7.4-fpm
MAINTAINER holmesian "i@holmesian.org"

#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && sed -i "s@http://deb.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && sed -i "s@http://security.debian.org@https://mirrors.aliyun.com@g" /etc/apt/sources.list

# WORKDIR /www
#COPY . .
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/

#  更新安装依赖包和PHP核心拓展
RUN apt-get update  \
    && apt-get install -y --no-install-recommends git libbz2-dev libmagickwand-dev libmcrypt-dev  zlib1g-dev  libzip-dev libfreetype6-dev libjpeg62-turbo-dev\
    && docker-php-ext-install -j$(nproc) gd bcmath zip pdo_mysql opcache mysqli\
    && pecl install imagick mcrypt-1.0.3 \
    && docker-php-ext-enable imagick mcrypt \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure opcache --enable-opcache \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -r /var/lib/apt/lists/*
        

# Donwload and install composer
RUN curl -sSL "https://getcomposer.org/installer" | php \
		&& mv composer.phar /usr/local/bin/composer


WORKDIR /www
RUN usermod -u 1000 www-data
