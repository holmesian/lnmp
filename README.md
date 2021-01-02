# lnmp

nginx  php7-fpm/php5-fpm  mysql  redis 的 docker 开发环境

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
    WWWROOTTYPE=rw  #For Win

    # mysql数据位置
    MYSQLDATA=/Users/holmesian/Docker/mysql

    # MYSQLDATA读写模式
    # MYSQLDATATYPE=delegated #For MAC
    MYSQLDATATYPE=rw  #For Win

    # mysql root密码
    # MYSQLPASWD={yourpasswd}



执行 docker-compose

    docker-compose up -d
    


# 备注

    - 默认为 php7.4 
    
    - 将 etc\nginx 配置文件中，fastcgi_pass php-fpm:9000 修改为 fastcgi_pass php5-fpm:9000 即可使用 php5
    
    - php / php5 目录下的 Dockerfile 为镜像配置文件，可酌情修改(可增加xdebug)，自行编译新镜像。
    
    - etc 目录中为相应的配置文件 
    
    - docker container 中的网站目录为 /www 

