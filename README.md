# lnmp

nginx  php7-fpm/php5-fpm  mysql  redis 的 docker 开发环境

![Docker Image CI](https://github.com/holmesian/lnmp/workflows/Docker%20Image%20CI/badge.svg?branch=master)


# 使用方法

下载到本地

    git clone https://github.com/holmesian/lnmp.git

    cd lnmp

    cp .env.sample .env

根据实际情况编辑 .env

    # web文件路径
    WWWROOT=/Users/holmesian/OneDrive/Coding/www

    # log文件路径
    LOGROOT=/Users/holmesian/Downloads/log

    # WWWROOT读写模式
    # WWWROOTTYPE=cached #For MAC
    #For Win
    WWWROOTTYPE=rw  

    # mysql数据位置
    MYSQLDATA=/Users/holmesian/Docker/mysql

    # MYSQLDATA读写模式
    # MYSQLDATATYPE=delegated #For MAC
    #For Win
    MYSQLDATATYPE=rw  

    # mysql root密码  默认 123456
    # MYSQLPASWD={yourpasswd}



执行 docker-compose  (docker-compose version >= 1.27)

    docker-compose up -d
    


# 备注

    - 默认为 php7.4 ;    docker version >= 19
    
    - 将 etc\nginx 配置文件中，fastcgi_pass php-fpm:9000 修改为 fastcgi_pass php5-fpm:9000 即可使用 php5
    
    - php / php5 目录下的 Dockerfile 为镜像配置文件，可酌情修改重新编译。需调试的环境可以选择holmesian/php5-fpm:xdebug  holmesian/php7-fpm:xdebug 
    
    - etc 目录中为相应的配置文件 （nginx/mysql/php）
    
    - docker container 中的网站根目录为 /www 

