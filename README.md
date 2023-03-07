# Docker for PHP Application

## Configuration

### NGINX

    copy default.conf.example to default.conf

    modify default.conf root value to your index file path in your application

    root /var/www/html/;

    root /var/www/html/test;


## Build

    docker-compose build

####  without cache

    add ---no-cache

## Up

    docker-compose up -d