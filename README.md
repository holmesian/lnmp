# lnmp

nginx  php-fpm  mysql xdebug docker 开发环境

# 使用方法

下载到本地

    git clone https://github.com/holmesian/lnmp.git

    cd lnmp

    cp .env.sample .env

根据实际情况编辑 .env

    #web文件路径
    WWWROOT={/c/Users/holmesian/OneDrive/Coding/www}

    #mysql数据位置
    MYSQLDATA={/c/Users/holmesian/OneDrive/AMD3600/Documents/docker/lnmp/mysql}

    #mysql root密码
    MYSQLPASWD={yourpasswd}

执行 docker-compose

    docker-compose up -d
    


# 备注

    - 默认为 php7.1 
    
    - 将 docker-compose.yml 中"image: holmesian/php7-fpm:v1"替换成"image: holmesian/php5-fpm:v1"即可使用PHP5
    
    - php / php5 目录下的 Dockerfile 为镜像配置文件，可酌情修改。
    
    - etc 目录中为相应的配置文件 
    
    - docker container 中的网站目录为 /www 

