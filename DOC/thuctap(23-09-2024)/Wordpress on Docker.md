# Wordpress on Docker


# Mục lục



- [Wordpress on Docker](#wordpress-on-docker)
- [Mục lục](#mục-lục)
- [I. Thiết lập môi trường Docker cho Wordpress](#i-thiết-lập-môi-trường-docker-cho-wordpress)
  - [1. Wordpress](#1-wordpress)
  - [2. Nginx](#2-nginx)
- [II. Cài đặt mã nguồn Wordpress thông qua các container của Docker](#ii-cài-đặt-mã-nguồn-wordpress-thông-qua-các-container-của-docker)
  - [1. Cài đặt các container](#1-cài-đặt-các-container)
  - [2. Cấu hình Nginx](#2-cấu-hình-nginx)
  - [3. PHP](#3-php)
- [III. Cài đặt Wordpress bằng các container của Docker](#iii-cài-đặt-wordpress-bằng-các-container-của-docker)
  - [1. Tạo thư mục dự án](#1-tạo-thư-mục-dự-án)
  - [2. Soạn thảo file YAML](#2-soạn-thảo-file-yaml)
    - [Thêm service Mariadb:](#thêm-service-mariadb)
    - [Thêm service Wordpress:](#thêm-service-wordpress)
    - [Thêm service Nginx:](#thêm-service-nginx)
    - [Thêm service PHP](#thêm-service-php)
    - [Thêm service phpMyAdmin](#thêm-service-phpmyadmin)
  - [3. Thêm các file cần thiết cho các container](#3-thêm-các-file-cần-thiết-cho-các-container)
- [IV. Cài đặt plugin và theme thông qua container wordpress](#iv-cài-đặt-plugin-và-theme-thông-qua-container-wordpress)
  - [1. Cài đặt thông qua wp-cli](#1-cài-đặt-thông-qua-wp-cli)
  - [2. Cài đặt thông qua bản zip](#2-cài-đặt-thông-qua-bản-zip)
- [END](#end)

# I. Thiết lập môi trường Docker cho Wordpress

Ta tạo một thư mục để chứa các mã nguồn Wordrpess, Nginx, PHP, Docker,... để tiện quản lí.

    # mkdir websitewp && cd websitewp 

## 1. Wordpress

Trong thư mục ``websitewp``, ta tải mã nguồn Wordpress về:

    # wget https://wordpress.org/latest.zip

Sau khi tải về các bạn dùng các công cụ giải nén nó ra, tại đây mình dùng unzip

    # unzip latest.zip

Xóa các file không cần thiết:

    # rm -rf wordpress latest.zip

## 2. Nginx

Cũng trong thư mục ``websitewp``, ta tạo thêm một thư mục Nginx để chứa file cấu hình của Nginx:

    # mkdir nginx && cd nginx

Trong thư mục ta tạo một file cấu hình nginx có tên ``default.conf``

    # touch default.conf

Bạn dùng trình soạn thảo ``vi`` hoặc ``nano`` để cấu hình file ``default.conf``:

    # nano default.conf

# II. Cài đặt mã nguồn Wordpress thông qua các container của Docker

Chúng ta quay lại thư mục ``websitewp``, tại thư mục ta tạo một file YAML docker để cài đặt các container cần thiết để chạy docker

    # touch docker-compose.yml

Bạn dùng soạn thoả vi hoặc nano để chỉnh sửa file ``docker-compose.yml``

    # nano docker-compose.yml

## 1. Cài đặt các container

Trong file ``docker-compose.yml`` ta sẽ soạn nội dung để cài đặt container cần thiết cho Wordpress.

```
    services:
        nginx:
            image: nginx:stable-alpine
            container_name: nginx
        

        mariadb:
            image: mariadb:latest
            container_name: mariadb
        
        
        php:
            image: php:8.2-fpm-alpine
            container_name: php_8.2
```
![](/thuctap/img/Docker_websitewp_docker_compose.png)

Chúng ta lưu lại và khi trong thư mục ``websitewp`` ta gõ lệnh để chạy file YAML

    # docker compose up           # Hoặc docker-compose up cho những phiên bản cũ hơn

Khi chúng ta gõ lệnh ``docker ps -a`` để liệt kê các container đang chạy ta sẽ thấy ở container mariadb sẽ có dòng trang thái là status: Exited

![](/thuctap/img/Docker_websitewp_docker_mariadb_error.png)

Trạng thái này nói lên Mariadb đã khởi động và sau đó dừng ngay. Chúng ta kiểm tra log để phát hiện lỗi:


    [root@localhost websitewp]# docker logs mariadb
    2024-09-30 07:51:20+00:00 [Note] [Entrypoint]: Entrypoint script for MariaDB Server 1:11.5.2+maria~ubu2404 started.
    2024-09-30 07:51:21+00:00 [Warn] [Entrypoint]: /sys/fs/cgroup///memory.pressure not writable, functionality unavailable to MariaDB
    2024-09-30 07:51:21+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
    2024-09-30 07:51:21+00:00 [Note] [Entrypoint]: Entrypoint script for MariaDB Server 1:11.5.2+maria~ubu2404 started.
    2024-09-30 07:51:21+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
            You need to specify one of MARIADB_ROOT_PASSWORD, MARIADB_ROOT_PASSWORD_HASH, MARIADB_ALLOW_EMPTY_ROOT_PASSWORD and MARIADB_RANDOM_ROOT_PASSWORD

Theo như log thông báo, tại đây ta thiếu các biến môi trường, cụ thể là ta không cung cấp mật khẩu root 

Ta dùng lệnh docker compose down để dừng các container:

    # docker compose down

Ta thêm môi trường vào container mariadb:

```
    mariadb:
     image: mariadb:latest
     container_name: mariadb
     environment:
      MYSQL_ROOT_PASSWORD: rootpass  # Mật khẩu cho root
      MYSQL_DATABASE: wordpress  # Tạo cơ sở dữ liệu wordpress
      MYSQL_USER: wp  # Tạo người dùng
      MYSQL_PASSWORD: wp_pass  # Mật khẩu cho người dùng
```
Sau đó ta chạy lại lệnh docker compose up. Và kiểm tra xem mariadb để chạy chưa.
    
    [root@localhost websitewp]# docker ps -a
    CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS                           PORTS                                       NAMES
    247fdb1b928a   mariadb:latest        "docker-entrypoint.s…"   53 seconds ago   Up 52 seconds                    3306/tcp                                    mariadb
    e0eee84c69db   nginx:stable-alpine   "/docker-entrypoint.…"   15 minutes ago   Up 15 minutes                    80/tcp                                      nginx
    6b6cd8272779   php:8.2-fpm-alpine    "docker-php-entrypoi…"   15 minutes ago   Up 15 minutes                    9000/tcp                                    php_8.2
    9be8945f426e   nginx                 "/docker-entrypoint.…"   2 hours ago      Exited (255) About an hour ago   0.0.0.0:80->80/tcp, :::80->80/tcp           lemp-docker-nginx-1
    495ba943540e   lemp-docker-php       "docker-php-entrypoi…"   2 hours ago      Exited (255) About an hour ago   9000/tcp                                    lemp-docker-php-1
    53588cf673bf   mariadb:latest        "docker-entrypoint.s…"   2 hours ago      Exited (255) About an hour ago   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp   lemp-docker-mariadb-1

Sau khi đã ổn thì ta truy cập vào localhost hoặc ip máy chủ mà docker của bạn đang chạy

![](/thuctap/img/Docker_websitewp_web_refuse.png)

Tại sao ta không thể kết nối được vào tên miền chúng ta ? Vì chúng ta chưa cấu hình mở port cho nginx, tiếp theo ta tới phần cấu hình Nginx

## 2. Cấu hình Nginx

Vì chúng ta chưa cấu hình port cho nginx, ta lại vào file docker-compose.yml để cấu hình container nginx:

```
    nginx:
     image: nginx:stable-alpine
     container_name: nginx
     ports:
      - 80:80  # Truy cập từ cổng 80, kiểm tường lửa xem có chặn cổng 80 không nếu có thì cho phép nginx đi qua
```

Ta thử truy cập lại localhost hoặc ip máy chủ mà docker đang chạy trên đó

![](/thuctap/img/Docker_LEMP_CheckNginx.png)

Sau khi đã chạy container nginx thành công, thì tiếp theo ta ánh xạ mã nguồn wordpress vào file YAML để chúng ta có thể cấu hình wordpress trên máy chủ.

* **Nginx**

```
  nginx:
    image: nginx:stable-alpine
    container_name: nginx
    ports:
      - 80:80
    volumes:
      - ./wordpress:var/www/html:delegated
```

* **PHP**

```
php:
    image: php:8.2-fpm-alpine
    container_name: php_8.2
    volumes:
      - ./wordpress:var/www/html:delegated
```
Chúng ta thử truy cập lại ip máy chủ của chúng ta.

![](/thuctap/img/Docker_LEMP_CheckNginx.png)

Vẫn không được.

Tại vì chúng ta chưa ánh xạ file cấu hình Nginx của chúng ta vào container Nginx, nếu chúng ta không ánh xạ tệp cấu hình Nginx vào container, Nginx sẽ sử dụng cấu hình mặc định và có thể không phục vụ đúng nhu cầu ta cần.

Ta soạn thảo file ``default.conf`` trong thư mục ``nginx`` mà ta tạo trước đó. sau đó thêm nội dung này vào trong file đó:

```
upstream php {
    server unix:/tmp/php-cgi.socket;
    server php:9000;
}


server {
    listen 80;
    server_name localhost;

    root /var/www/html;  

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args; 
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass php;  # Sử dụng nhóm upstream đã định nghĩa
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

Sau đó ta quay lại file YAML thêm dòng này vào trong volumes của nginx

```
- ./wordpress:/var/www/html:delegated
```

Ta thử truy cập lại ip của máy chủ

![](/thuctap/img/Docker_websitewp_need_mysqli.png)

Tại đây đang thông báo ta đang thiếu các MySQL extension của PHP

## 3. PHP

Ta tạo một docker file để tạo một image php8.2 và thêm các extension của nó.

    # touch php.dockerfile

Ta soạn nội dung sau vào trong file php.dockerfile:

```
FROM php:8.2-fpm-alpine

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo pdo_mysql

```

Ta vào file YAML để chỉnh sửa phần container php:

```
 php:
    build:
      context: .
      dockerfile: php.dockerfile
    container_name: php_8.2
    volumes:
      - ./wordpress:/var/www/html:delegated
```
Ta chạy lệnh:

    # docker compose up -d --build

Ta thử truy cập lại ip máy chủ

![](/thuctap/img/Docker_websitewp_wordpress.png)

# III. Cài đặt Wordpress bằng các container của Docker

Phần II là phần bạn đã có mã nguồn Wordpress để cài đặt thông qua các container. Giờ tiếp theo ta sẽ cài đặt Wordpress bằng các container trên Docker.

## 1. Tạo thư mục dự án

Để tránh xung đột với dự án ở phần II, các bạn tạo một thư mục khác để chứa dự án ở phần III này

    # mkdir wp-project

Trong thư mục ``wp-project``, các bạn hãy tạo một file YAML như phần II.

    # touch docker-compose.yml

Định nghĩa biến môi trường. Khi thực thi, các container WordPress và MySQL sử dụng biến môi trường nhằm đảm bảo khả năng truy cập ứng dụng và tính nhất quán dữ liệu.

    # nano .env

Các bạn sao chép nội dung này vào trong file ``.env``

    MYSQL_ROOT_PASSWORD: rootpass  
    MYSQL_DATABASE: wordpress 
    MYSQL_USER: wp  
    MYSQL_PASSWORD: wp_pass  

## 2. Soạn thảo file YAML

### Thêm service Mariadb:

```
services:
  mariadb:
    image: mariadb:latest
    container_name: mariadb
    restart: unless-stopped
    env_file: .env
    volumes:
      - mariadb:/var/lib/mysql
    
```
### Thêm service Wordpress:

```
  wordpress:
    depends_on: 
      - mariadb
    image: wordpress:latest
    container_name: wordpress
    restart: unless-stopped
    env_file: .env
    ports:
      - "80:80"
    environment:
      - WORDPRESS_DB_HOST=mariadb:3306
      - WORDPRESS_DB_USER=${MYSQL_USER}
      - WORDPRESS_DB_PASSWORD=${MYSQL_PASSWORD}
      - WORDPRESS_DB_NAME=${MYSQL_DATABASE}
    volumes:
      - wordpress:/var/www/html
```

### Thêm service Nginx:

```
  nginx:
    depends_on:
      - wordpress
    image: nginx:latest
    container_name: webserver
    restart: unless-stopped
    volumes:
      - wordpress:/var/www/html
      - ./nginx:/etc/nginx/conf.d
      - certbot-etc:/etc/letsencrypt

```

### Thêm service PHP
```
  php:
    image: php:8.2-fpm-alpine
    container_name: php_8.2
    restart: unless-stopped
    volumes:
      - ./wordpress:/var/www/html:delegated
```

### Thêm service phpMyAdmin

```
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin
    restart: unless-stopped
    ports:
      - "8080:80"
    environment:
      - PMA_HOST=mariadb
      - PMA_USER=${MYSQL_USER}
      - PMA_PASSWORD=${MYSQL_PASSWORD}
    depends_on:
      - mariadb
```

## 3. Thêm các file cần thiết cho các container

Trong phần container Nginx ta có gắn thư mục ``./nginx/default.conf`` vào ``/etc/nginx/conf.d`` trong container Nginx

Tạo thư mục Nginx:

    # mkdir nginx && cd nginx

Tạo file default.conf:

    # nano default.conf

Các bạn sao chép nội dùng vào file ``default.conf``:

```
upstream php {
    server php:9000;  
}

server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass php;  
        fastcgi_param PATH_INFO $fastcgi_path_info;
        include fastcgi_params;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }


    location ~ /\.ht {
        deny all;
    }

    location ~* /(\.htaccess|\.htpasswd|\.git|\.svn|\.env|\.DS_Store|\.idea|\.vscode) {
        deny all;
    }

    # Cấu hình cho phpMyAdmin
    location /phpmyadmin {
        alias /var/www/html/phpmyadmin;  
        index index.php index.html index.htm;

        location ~ ^/phpmyadmin/(.*\.php)$ {
            fastcgi_pass php;  
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $request_filename;
            include fastcgi_params;
        }
    }
}
```

Sau khi đã cấu hình đầy đủ các bạn gõ lệnh sau để khởi chạy:

    # docker compose up -d 

![](/thuctap/img/Docker_wp-project_wordpress.png)

![](/thuctap/img/Docker_wp-project_phpmyadmin.png)

# IV. Cài đặt plugin và theme thông qua container wordpress

## 1. Cài đặt thông qua wp-cli

Để sử dụng được ``wp-cli`` các bạn phải vào trong container wordpress của dự án của các bạn.

    # docker exec -it <Tên container hoặc container ID> bash

Nếu các bạn chưa cài đặt wp-cli trong container wordpress các bạn thực hiện lần lượt các lệnh sau để cài đặt

Sử dụng lệnh sau để tải WP-CLI:

    # curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

Cấp quyền thực thi:

    # chmod +x wp-cli.phar

Di chuyển vào thư mục bin:

    # mv wp-cli.phar /usr/local/bin/wp

Kiểm tra cài đặt:

    # wp --info

![](/thuctap/img/Docker_WP_CLI_Install.png)

Sau khi đã cài đặt xong thì chúng ta thử cài đặt plugin bằng wp-cli. Tại bài lad này mình thử cài đặt 1 một plugin có tên Classic Editor. Tại ảnh dưới là hình ảnh plugin chưa cài đặt

![](/thuctap/img/Docker_WP_CLI_NotYet.png)

Để chạy được các lệnh ``wp-cli`` các bạn phải ở trong thư mục gốc của Wordpress, đa số theo mặc định nó sẽ nằm trong đường dẫn ``/var/www/html``

Các bạn nhập lệnh sau để cài đặt:

    # wp plugin install classic-editor --activate --allow-root

Trong đó:

* ``wp``: Đây là lệnh gọi đến WP-CLI, cho phép bạn thực hiện các tác vụ quản lý WordPress từ dòng lệnh.

* ``plugin``: Đây là một phần của lệnh, cho WP-CLI biết rằng bạn đang muốn thực hiện các thao tác liên quan đến plugin.

* ``install``: Đây là hành động bạn muốn thực hiện - cài đặt một plugin.

* ``classic-editor``: Đây là tên của plugin mà bạn muốn cài đặt. Trong trường hợp này, "Classic Editor" là plugin giúp bạn sử dụng trình soạn thảo cổ điển thay vì trình soạn thảo khối (Gutenberg) mà WordPress mới sử dụng.

* ``--activate``: Đây là một tùy chọn, cho WP-CLI biết rằng bạn không chỉ muốn cài đặt plugin mà còn muốn kích hoạt nó ngay lập tức sau khi cài đặt. Nếu bạn không sử dụng tùy chọn này, bạn sẽ cần kích hoạt plugin thủ công sau khi cài đặt.

* ``--allow-root``: Tùy chọn này cho phép bạn chạy WP-CLI với quyền root. Theo mặc định, WP-CLI không cho phép chạy với quyền root vì lý do bảo mật, nhưng nếu bạn thực sự cần làm như vậy, bạn có thể sử dụng tùy chọn này. Tuy nhiên, việc này có thể tiềm ẩn rủi ro, vì bất kỳ mã nào chạy trên trang của bạn cũng sẽ có quyền truy cập đầy đủ vào máy chủ.

![](/thuctap/img/Docker_WP_CLI_PluginSuccess.png)

![](/thuctap/img/Docker_WP_CLI_CheckPlugin.png)

Thông thường khi cài đặt plugin bằng wp-cli thì nó sẽ chứa vào trong đường dẫn `/var/www/html/wp-content/plugins/`

![](/thuctap/img/Docker_WP_CLI_CheckPlugin_Folder.png)

Tương tự như làm với theme wordpress khi ta dùng wp-cli thì theme sẽ được chứa trong đường dẫn ``/var/www/html/wp-content/themes/``

Mình sẽ thử cài đặt theme ``OceanWP`` bằng wp-cli. Chúng ta hãy quay lại thư mục gốc của wordpress để cài đặt.

    # wp theme install oceanwp --active --allow-root

![](/thuctap/img/Docker_WP_CLI_ThemeSucces.png)

![](/thuctap/img/Docker_WP_CLI_ThemeCheck.png)

![](/thuctap/img/Docker_WP_CLI_ThemeCheck_Folder.png)

## 2. Cài đặt thông qua bản zip

Cài thông qua bản ZIP khác với khi chúng ta dùng wp-cli cài đặt plugin và theme thì nó sẽ tự động đưa vào các thư mục chứa plugin và theme của wordpress. Còn cài đặt từ bản zip thì yêu cầu chúng ta phải tự di chuyển đúng theme và lgin vào đúng trong thư mục đó. Nhưng bù lại chúng ta có thể tải plugin và theme ở bất kì đâu không như wp-cli bị giới hạn ở kho lưu trữ Wordpress

Nếu các bạn chưa cài đặt lệnh unzip thì các bạn gõ lệnh sau để cài đặt:

    # apt update && apt install unzip -y

Mình sẽ thử cài đặt theme Soledad thông qua đường link: https://tool.dotrungquan.info/wordpress/theme/Soledad-v8.1.9.zip

Chúng ta di chuyển vào thư mục theme:

    # cd /var/www/html/wp-content/themes

Sử dụng lệnh curl để tải tệp ZIP của theme Soledad từ link trên:

    # curl -O https://tool.dotrungquan.info/wordpress/theme/Soledad-v8.1.9.zip

Giải nén tệp ZIP sau khi tải xong:

    # unzip Soledad-v8.1.9.zip

Tuỳ vào bản theme sẽ có các cách kích hoạt khác nhau. Ví dụ như theme Soledad các bạn giải nén xong các bạn phải vào thư mục ``Soledad_WordPress_Theme_v8.1.9``, trong đó sẽ có hai file zip là ``soledad.zip`` và ``soledad-child.zip``

Các bạn phải giải nén 2 thư mục này ra ngoài đường dẫn ``/var/www/html/wp-content/themes/`` thì mới kích hoạt được theme

    # unzip soledad.zip -d /var/www/html/wp-content/themes/

Sau khi giải nén ta kích hoạt theme bằng wp-cli:

    # wp theme activate soledad --allow-root

![](/thuctap/img/Docker_ZIP_Soledad_Switch.png)

![](/thuctap/img/Docker_ZIP_Soledad_WEB.png)


Tương tự như theme chúng ta cũng cài plugin bằng tệp zip. Mình sẽ thử cài plugin bằng tệp zip bằng link này: https://tool.dotrungquan.info/wordpress/mythemeshop-plugins/mts-wp-google-translate.zip

Chúng ta vào thư mục plugin của wordpress;

    # cd /var/www/html/wp-content/plugins/

Sử dụng lệnh curl để tải tệp ZIP của plugin từ link trên:

    # curl -O https://tool.dotrungquan.info/wordpress/mythemeshop-plugins/mts-wp-google-translate.zip

Giải nén tệp tin vừa tải về:

    # unzip mts-wp-google-translate.zip -d /var/www/html/wp-content/plugins/

Sau khi giải nén ta kích hoạt plugin lên:

    # wp plugin activate mts-wp-google-translate --allow-root

![](/thuctap/img/Docker_ZIP_Plugin_Check.png)

![](/thuctap/img/Docker_ZIP_Plugin_CheckWeb.png)

# END