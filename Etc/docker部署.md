### docker安装XXL-JOB
    docker run -d \
    -e PARAMS="--spring.datasource.url=jdbc:mysql://mysql:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai --spring.datasource.username=root --spring.datasource.password=123456" \
    -p 11000:8080 \
    -v /Users/zhangxs/DockerVolumes:/data/applogs \
    --link mysql \
    --name xxl-job-admin \
    xuxueli/xxl-job-admin:2.3.0

### 安装wordpress
    docker run -d --link mysql \
    -e WORDPRESS_DB_HOST=mysql \
    -e WORDPRESS_DB_USER=root \
    -e WORDPRESS_DB_PASSWORD=123456 \
    -e WORDPRESS_DB_NAME=wordpress \
    -v /Users/zhangxs/DockerVolumes/wordpress:/var/www/html \
    -p 9999:80 \
    --add-host=webhook.test:192.168.99.227 \
    --name wordpress \
    wordpress:5
