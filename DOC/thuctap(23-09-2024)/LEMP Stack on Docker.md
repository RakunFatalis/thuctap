# LEMP Stack on Docker

# Mục lục

# I. Cài đặt LEMP Stack
Trong bài lab ta sử dụng:

  Máy ảo: CentOS 9.
    
  Địa chỉ ip của máy ảo: 192.168.0.200

  Đã cài sẵn Docker và Docker compose

**Bước 1. Tạo thư mục và các file cần thiết cần thiết**

Ta cần tạo một thư mục để chứa các dự án của docker. Thư mục này sẽ chứa tất cả các file liên quan đến dự án, bao gồm file cấu hình docker-compose.yml, mã nguồn, và các file khác như cấu hình cho các dịch vụ.

Ta nhập câu lệnh sau để tạo:

    # mkdir lemp-docker && cd lemp-docker

Bên trong thư mục này, tạo file ``docker-compose.yml``:

    # nano docker-compose.yml

**Bước 2. Cấu hình docker-compose.yml**

Sau khi ta đã tạo docker-compose.yml, ta thêm nội dung này vào trong file:
  
version: '3.7'

    services:
      nginx:
        image: nginx
        ports:
          - "80:80"
        volumes:
          - ./nginx.conf:/etc/nginx/conf.d/default.conf
        depends_on:
          - php
        networks:
          - lemp-net

      php:
        build: .
        volumes:
          - ./src:/var/www/html
        depends_on:
          - mariadb
        networks:
          - lemp-net

      mariadb:
        image: mariadb:latest
        environment:
          MYSQL_ROOT_PASSWORD: rootpassword
          MYSQL_DATABASE: database
          MYSQL_USER: hailong
          MYSQL_PASSWORD: hailong123
        ports:
          - "3306:3306"
        volumes:
          - db_data:/var/lib/mysql
        networks:
          - lemp-net

    volumes:
      db_data:

    networks:
      lemp-net:

![](/img/Docker_LEMP_FileCompose.png)

Vì trong file docker-compose.yml chúng ta sử dụng build cho php nên ta cần tạo một Docker File cho php.

    # nano Dockerfile

Ta thêm nội dung này vào trong Dockerfile:

    # Chỉ định image cơ sở
    FROM php:8.2-fpm-alpine

    # Cài đặt các extension PHP cần thiết
    RUN apk add --no-cache libzip-dev && \
        docker-php-ext-install zip mysqli pdo_mysql

    # Thiết lập thư mục làm việc
    WORKDIR /var/www/html

    # Sao chép các tệp cấu hình PHP (nếu có)
    COPY php.ini /usr/local/etc/php/

    # Sao chép code ứng dụng vào container
    COPY . .

![](/img/Docker_LEMP_DockerFile.png)

**Bước 3: Tạo thư mục và các file cần thiết của Nginx:**

Tạo file cấu hình Nginx:

    nano nginx.conf

Thêm nội dung này vào trong file cấu hình:

    server {
        listen 80;
        server_name localhost;

        root /var/www/html;  # Đường dẫn đến thư mục mã nguồn PHP
        index index.php index.html index.htm;

        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
            include fastcgi_params;
            fastcgi_pass php:9000;  # Kết nối đến dịch vụ PHP
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }


![](/img/Docker_LEMP_NginxConfig.png)

**Bước 4: Tạo thư mục chứa mã nguồn web:**

Tạo thư mục src để chứa mã nguồn PHP trong đó có chứa file index.php:

    # mkdir src
    # touch src/index.php

Ta thêm nội dung này vào trong index.php:

    <?php
    phpinfo();
    ?>

Ta tạo thêm file php.ini cho Docker file;

    # touch php.ini


**Bước 5: Chạy docker compose và Docker file:**

Trước khi chạy docker compose ta cần mở các cổng mặc định của Nginx với MariaDB:

    # firewall-cmd --add-port=80/tcp --permanent
    # firewall-cmd --add-port=3306/tcp --permanent
    # firewall-cmd --reload

Chạy file Dockerfile:

    # docker build -t php8.2 .

![](/img/Docker_LEMP_Build.png)

Chạy file compose

    # docker compose up -d --build

![](/img/Docker_LEMP_RunDockerCompose.png)


# II. Kiểm tra

Sau khi chạy docker compose up, có một số điều quan trọng bạn nên kiểm tra để đảm bảo rằng các dịch vụ của bạn đã khởi động thành công và hoạt động đúng cách.

Kiểm tra web Nginx

![](/img/Docker_LEMP_CheckNginx.png)

Kiểm tra các container

    # docker ps

![](/img/Docker_LEMP_ps.png)

Kiểm tra phiên bản PHP:

    # nano src/info.php  # Tạo file info.php trong thư mục src để kiểm tra phiên bản

Nội dung của file info.php sẽ như sau:

    <?php
    phpinfo();
    ?>

![](/img/Docker_LEMP_info_php.png)

# END