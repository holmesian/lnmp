FROM php:5.6-fpm
MAINTAINER holmesian "i@holmesian.org"

#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 国内网络增加下列
# RUN sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
    # && sed -i "s@http://security.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list 

# WORKDIR /www
# 测试用
#COPY . .
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/

#  更新安装依赖包和PHP核心拓展
RUN apt-get update --fix-missing \
    && apt-get install -y --no-install-recommends git libbz2-dev libmagickwand-dev libmcrypt-dev  zlib1g-dev  libzip-dev libfreetype6-dev libjpeg62-turbo-dev\
    && docker-php-ext-install -j$(nproc) gd bcmath zip pdo_mysql opcache mysqli mcrypt \
    && pecl install imagick-beta\
    && docker-php-ext-enable imagick mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure opcache --enable-opcache \
    && rm -r /var/lib/apt/lists/*
        

WORKDIR /www
RUN usermod -u 1000 www-data
