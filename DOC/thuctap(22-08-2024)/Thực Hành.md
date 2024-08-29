# LEMP Stack trên Ubuntu 20.04 và WordPress


# Mục lục
- [LEMP Stack trên Ubuntu 20.04 và WordPress](#lemp-stack-trên-ubuntu-2004-và-wordpress)
- [Mục lục](#mục-lục)
- [I. Chuẩn bị](#i-chuẩn-bị)
  - [Thiết lập sủ dụng SSH Key trên Linux](#thiết-lập-sủ-dụng-ssh-key-trên-linux)
  - [Thiết lập sủ dụng SSH Key trên Window](#thiết-lập-sủ-dụng-ssh-key-trên-window)
  - [Đổi port SSH sang 2024](#đổi-port-ssh-sang-2024)
- [II. Cài đặt LEMP](#ii-cài-đặt-lemp)
  - [1. Cài đặt Nginx\*\*](#1-cài-đặt-nginx)
  - [2. PHP-FPM pools](#2-php-fpm-pools)
  - [3. Cài đặt Maria DB bản mới nhất](#3-cài-đặt-maria-db-bản-mới-nhất)
  - [4. Cài đặt phpMyadmin](#4-cài-đặt-phpmyadmin)
  - [5. Certbot](#5-certbot)
- [END](#end)

# I. Chuẩn bị

Một VPS Ubuntu có địa chỉ IP: ``103.110.85.87``

## Thiết lập sủ dụng SSH Key trên Linux

 Để tạo SSH Key ta nhập lệnh sau: ``ssh-keygen -t rsa`` để tạo chuổi Public key và Private key ở máy khách.

 ![](/thuctap/img/VPS_SSHKey.png)

Trong thông báo bạn sẽ thấy 2 dòng:

**Your identification has been saved in ``name_key``**: Đây là thông báo cho bạn biết rằng khóa riêng tư (Private key) của bạn đã được lưu trong tệp.

**Your Public key has been saved in ``name_key.pub``**: Đây là thông báo cho bạn biết rằng khóa công khai (Public key) đã được lưu trong tệp

Thông thường khi bạn nhập lệnh tạo SSH Key thì Public key và Private key lưu tại thư mục ``.ssh`` mà bạn nhập lệnh, ta dùng lệnh ``ls -al`` để in các tệp có trong thư mục ra.

![](/thuctap/img/VPS_2Key.png)

Tiếp theo ta thêm Public key lên VPS. Bạn hãy ssh vào VPS với thông tin passwd root và thực hiện nhập tuần tự các lệnh sau.

    # mkdir ~/.ssh                      Tạo thư mục .ssh 
    # chmod 700 ~/.ssh                  Đặt quyền truy cập cho thư mục .ssh thành 700.
    # touch ~/.ssh/authorized_keys      Tạo một tệp rỗng có tên authorized_keys trong thư mục .ssh
    # chmod 600 ~/.ssh/authorized_keys  Đặt quyền truy cập cho tệp authorized_keys thành 600

Những lệnh này thiết lập môi trường bảo mật cho SSH bằng cách tạo thư mục và tệp cần thiết và cấu hình các quyền truy cập phù hợp. Điều này giúp bảo vệ dữ liệu xác thực SSH của bạn khỏi các truy cập trái phép và đảm bảo rằng chỉ có người dùng được phép mới có thể kết nối qua SSH.


* **Copy Public key bằng cách thủ công**

  Trên con máy có chứa Public key của bạn, bạn mở terminal và chạy lệnh ``cat`` để hiển thị nội dung của khoá và copy nó.

  ![](/thuctap/img/VPS_CatPub.png)

  Bạn SSH tới VPS như bằng cách sử dụng lệnh: ``# ssh user@ip_server``

  Trong đó: 
  
    * ``user``: Tên người dùng trên máy chủ từ xa mà bạn muốn đăng nhập.

    * ``ip_server``: Địa chỉ IP hoặc tên miền của máy chủ từ xa mà bạn muốn kết nối đến.
  
  Sau đó ta sử dụng lệnh: ``# nano ~/.ssh/authorized_keys`` để mở thư mục ``authorized_keys`` và dán key đã copy vào.

  ![](/thuctap/img/VPS_SSHCopy.png)

  Để sử dụng SSH key, ta mở Terminal lên và sử dụng lệnh sau để SSH:

  ``# ssh -i duong_dan_chua_Private_key root@ip_may_chu -p port_SSH``

  ![](/thuctap/img/VPS_SSH_Succes.png)

  Sau khi đã SSH key thành công bạn có thể tắt cho phép SSH bằng Passwd đi để tránh do passwd và brute force attack nhé. Để tắt đăng nhập ssh bằng passwd bạn thực hiện như sau. Bạn mở file ``/etc/ssh/sshd_config`` sau đó tìm đến dòng ``PasswordAuthentication Yes`` bạn chuyển thành ``PasswordAuthentication no``

  ![](/thuctap/img/VPS_yestono.png)

  Sau khi lưu xong bạn đừng quên khởi động lại dịch vụ ssh.

  ``# systemctl restart sshd``

## Thiết lập sủ dụng SSH Key trên Window

Ngoài cách sử dụng command line trên Linux ngoài ra ta còn có cách khác là sử dụng phần mềm Putty để tạo SSH key và sử dụng SSH key đó để đăng nhập vào VPS.

* **Tạo SSH key bằng PuttyGen**

  ![](/thuctap/img/VPS_Putty_Gene.png)


  ![](/thuctap/img/VPS_Putty_Click.png)

  ![](/thuctap/img/VPS_Putty_SaveKey.png)

* **Sử dụng SSH Key trên Putty**

  Bạn mở PuTTY lên sau đó click vào SSH => Auth. Tiếp đến bạn clck vào Browse để tìm đến file Private key đã tạo và lưu.. Khi đã trỏ được đến file Private và bạn thực hiện SSH thì bạn sẽ nhận được yêu cầu nhập vào Passphrase, bạn hãy nhập Passphrase để hoàn tất bước SSH nhé.

  ![](/thuctap/img/VPS_Putty_Connect.png)

## Đổi port SSH sang 2024

Mở tệp cấu hình SSH (``/etc/ssh/sshd_config``) bằng trình soạn thảo văn bản:

``# nano /etc/ssh/sshd_config``

Tìm dòng có nội dung ``#Port 22``. Bỏ dấu ``#`` và thay đổi số 22 thành 2024:

![](/thuctap/img/VPS_Port2024.png)

Mở cổng 2024 trên tường lửa:

``# ufw allow 2024/tcp``

``# ufw enable``

Khởi động lại dịch vụ SSH để áp dụng các thay đổi:

``# systemctl restart sshd``


# II. Cài đặt LEMP

## 1. Cài đặt Nginx**

  Nginx là một máy chủ web phổ biến được sử dụng để phục vụ các trang web, nhưng nó còn có khả năng hoạt động như một máy chủ proxy ngược (reverse proxy), cân bằng tải (load balancer), và proxy email (IMAP/POP3)

  * **Bước 1: Cài đặt Nginx**

    Một điều vô cùng quan trọng trước khi cài một phần mềm mới, bạn phải cập nhật danh sách repository của mình.

    ``# apt update -y``

    Sau khi hoàn thành cập nhật thì bạn gõ lệnh:

    ``# apt install nginx -y``

    Tiếp theo bạn hãy kiểm tra xem nginx đã cài đặt chưa bằng lệnh:

    ``# nginx -v``

    Nó sẽ trả ra kết quả như sau:

    ![](/thuctap/img/nginx_v_2.png)

    * **Bước 2: Cho phép các port HTTP và HTTPS.**

    Bạn cần phải cấu hình tường lửa để Nginx có thể đáp ứng dịch vụ qua internet. Thông thường CentOS sẽ mặc định chặn truy cập vào port 80 và 443, điều này sẽ trực tiếp chặn các traffic của Nginx. Để cho phép các traffic HTTP và HTTPS ta thực thi lần lượt các lệnh sau:

    ``# ufw allow 80/tcp`` 

    ``# ufw allow 443/tcp``

    ``# ufw reload``

    Để xác nhận rằng các quy tắc đã được áp dụng thành công, bạn có thể kiểm tra trạng thái của ufw bằng lệnh:

    ``# ufw status``

  * **Bước 3: Khởi động dịch vụ Nginx:**

    Sau khi cài đặt xong, khởi động dịch vụ Nginx và kiểm tra dịch vụ đã chạy chưa

    ``# systemctl start nginx``

    ``# systemctl status nginx``

  * **Bước 4: Nhập IP Server để kiểm tra:**

    Sau khi các bạn cài đặt thành công xong thì các bạn nhập IP Server của các bạn để kiểm tra xem ta đã cài đặt thành công chưa:

    ![](/thuctap//img/Nginx_success_v2.png)

## 2. PHP-FPM pools

  PHP-FPM (**PHP FastCGI Process Manager**) là một phiên bản nâng cao của FastCGI để chạy các ứng dụng PHP. Một trong những tính năng quan trọng của PHP-FPM là pools, cho phép quản lý nhiều nhóm tiến trình PHP độc lập trên cùng một máy chủ. Mỗi pool có thể có các cấu hình riêng biệt, bao gồm số lượng tiến trình, người dùng chạy tiến trình, và các tham số tối ưu hóa khác.

  Sau đây mình sẽ làm lab tạo 2 vhost sử dụng hai phiên bản PHP khác nhau, cụ thể:

  **vhost website1.dns.info.vn (php 8.2)**

  **vhost website2.dns.info.vn (php 7.4)**


  * **Bước 1: Cài đặt PHP-FPM**

    Cài đặt PHP-FPM và các phiên bản PHP:

    ``# apt update``
    
    ``# apt install php8.2-fpm php7.4-fpm -y``

    Nếu như trong quá trình cài đặt bạn có gặp thông báo lỗi này:

        E: Unable to locate package php8.2-fpm
        E: Couldn't find any package by glob 'php8.2-fpm'
        E: Package 'php7.4-fpm' has no installation candidate

    Thì lỗi này thường xảy ra khi hệ thống không thể tìm thấy các gói PHP cụ thể trong kho lưu trữ hiện tại của bạn. Bạn thêm câu lệnh này để khắc phục:

    ``# add-apt-repository ppa:ondrej/php``: Lệnh này để thêm PPA (Personal Package Archive) vào hệ thống Ubuntu của bạn.

    Sau khi thêm vào xong bạn gõ lại lệnh cài đặt ở trên.

    Tiếp theo ta cài đặt các module phổ biến của hai phiên bản PHP:

    ``# apt install php8.2-mysql php7.4-mysql php8.2-xml php7.4-xml php8.2-curl php7.4-curl -y``

  * **Bước 2: Cấu hình Pool:**

    Cấu Hình Pool cho PHP 8.2

    Thông thường file cấu hình cho pool nằm tại: ``/etc/php/8.2/fpm/pool.d/website1.conf`` nếu chưa có thì ta dùng câu lệnh sau để tạo và cấu hình:

    ``# nano /etc/php/8.2/fpm/pool.d/website1.conf``

    Bạn cấu hình như sau:

    ![](/thuctap/img/VPS_PHP_Pool_8_2.png)

    Trước khi ta tiếp tục thì ta hãy tìm hiểu từng thành phần trong file cấu hình pool:

    | Cấu hình| Giải thích|
    |-------------|-----------|
    | `[website1]`| Tên của pool PHP-FPM, giúp phân biệt và quản lý các cấu hình khác nhau.|
    | `user = www-data`| Người dùng mà PHP-FPM sẽ chạy dưới quyền. `www-data` thường là người dùng mặc định cho các dịch vụ web trên Ubuntu. |
    | `group = www-data`| Nhóm mà PHP-FPM sẽ chạy dưới quyền. `www-data` cũng là nhóm mặc định cho các dịch vụ web trên Ubuntu.|
    | `listen = /run/php/php8.2-fpm-website1.sock`| Địa chỉ socket Unix mà PHP-FPM lắng nghe các yêu cầu từ web server. Sử dụng socket Unix thay vì cổng TCP.|
    | `listen.owner = www-data`| Quyền sở hữu cho socket Unix. Đảm bảo web server có quyền truy cập đến socket.|
    | `listen.group = www-data`| Nhóm sở hữu socket Unix. Đảm bảo web server có quyền truy cập đến socket.|
    | `pm = dynamic`| Phương pháp quản lý số lượng tiến trình con. `dynamic` giúp tự động điều chỉnh số lượng tiến trình dựa trên nhu cầu. |
    | `pm.max_children = 10`| Số lượng tối đa các tiến trình con có thể tạo ra. Giới hạn này giúp quản lý tải và hiệu suất.                       |
    | `pm.start_servers = 2`| Số lượng tiến trình con khởi động khi PHP-FPM bắt đầu. Đảm bảo có sẵn tiến trình để xử lý yêu cầu ngay từ đầu.        |
    | `pm.min_spare_servers = 1`|Số lượng tiến trình con tối thiểu duy trì để xử lý yêu cầu mới. Nếu ít hơn, PHP-FPM sẽ tạo thêm tiến trình.|
    | `pm.max_spare_servers = 5` | Số lượng tiến trình con tối đa duy trì khi không có yêu cầu mới. Nếu quá nhiều, PHP-FPM sẽ tiêu diệt các tiến trình thừa.|
    | `chdir = /`| Thư mục làm việc hiện tại cho các tiến trình PHP. `chdir = /` có nghĩa là thư mục gốc của hệ thống.|
    
    Ta làm tương tự với PHP 7.4

    Sau khi tạo các file cấu hình này, bạn cần khởi động lại dịch vụ PHP-FPM để áp dụng các thay đổi:

    ``# systemctl restart php8.2-fpm``
    
    ``# systemctl restart php7.4-fpm``

  * **Bước 3: Tạo Virtual Hosts (vhost)**

    Virtual Hosts là một phương thức lưu trữ cho phép lưu nhiều tên miền khác nhau trên cùng một máy chủ Server. Virtual Hosts có thể được xem như một giải pháp cho phép bạn nhúng rất nhiều tên miền trên một địa chỉ IP của một Server duy nhất. Tùy vào cách cài đặt, Server sẽ tự hiểu tên miền nào đang hoạt động bên trong vị trí lưu trữ của Server.

    Virtual Hosts được xem là một giải pháp khá hiệu quả và tiết kiệm chi phí hơn khi sử dụng nhiều tên miền chỉ trên một địa chỉ IP của Server.

    **Cấu hình vhost cho hai website**

    Ta sẽ tạo 1 file cấu hình vhost cho ``website1.dns.info.vn``:

    ``# nano /etc/nginx/sites-available/website1.dns.info.vn``

    Ta thêm nội dung này vào trong file:

        server {
        listen 80;
        server_name website1.dns.info.vn;
        root /var/www/website1.dns.info.vn;
        index index.php index.html index.htm;

        location / {
            try_files $uri $uri/ =404;
          }

        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/run/php/php8.2-fpm.sock;
          }

        location ~ /\.ht {
            deny all;
          }
        }   

    Giải thích file cấu hình này:

        server {
        listen 80;
        server_name website1.dns.info.vn;
        root /var/www/website1.dns.info.vn;
        index index.php index.html index.htm;
    
    **server { }**: Định nghĩa một khối cấu hình cho một server (virtual host).

    **listen 80;**: Nginx sẽ lắng nghe trên cổng 80 cho các kết nối HTTP. Đây là cổng mặc định cho HTTP.

    **server_name website1.dns.info.vn;**: Xác định tên miền mà server block này sẽ xử lý. Trong trường hợp này là website1.dns.info.vn.

    **root /var/www/website1.dns.info.vn;**: Chỉ định thư mục gốc nơi chứa các file của website. Đây là thư mục mà Nginx sẽ sử dụng để tìm các file khi có yêu cầu từ client.

    **index index.php index.html index.htm;**: Xác định danh sách các file mặc định mà Nginx sẽ tìm và phục vụ khi không có tên file cụ thể nào được yêu cầu. Ví dụ, nếu người dùng truy cập vào ``http://website1.dns.info.vn/``, Nginx sẽ cố gắng phục vụ index.php, index.html, hoặc index.htm theo thứ tự.

        location / {
        try_files $uri $uri/ =404;
        }

    **location / { }**: Xác định khối cấu hình cho tất cả các yêu cầu tới thư mục gốc của website (root directory).

    ``try_files $uri $uri/ =404;``: Cố gắng phục vụ file được yêu cầu bởi client ($uri). Nếu không tìm thấy, thử phục vụ như một thư mục ($uri/). Nếu cả hai không thành công, trả về mã lỗi 404 (Not Found).

        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
        }

    **location ~ .php$ { }**: Xác định khối cấu hình cho tất cả các yêu cầu tới các file có phần mở rộng .php.

    **include snippets/fastcgi-php.conf;**: Bao gồm các cấu hình chuẩn cho PHP-FPM từ file fastcgi-php.conf. File này thường bao gồm các thông số liên quan đến FastCGI như fastcgi_param, fastcgi_index, v.v.

    **fastcgi_pass unix:/run/php/php8.2-fpm.sock;**: Chuyển tiếp (proxy) các yêu cầu PHP tới PHP-FPM thông qua socket Unix (/run/php/php8.2-fpm.sock). Đây là nơi PHP-FPM lắng nghe các yêu cầu để xử lý chúng.


        location ~ /\.ht {
        deny all;
        }

    **location ~ /.ht { }**: Xác định khối cấu hình cho tất cả các yêu cầu tới các file bắt đầu bằng .ht.

    **deny all;**: Chặn tất cả các truy cập vào các file có tiền tố .ht. Điều này thường được sử dụng để bảo vệ các file cấu hình .htaccess (nếu có), giúp tránh việc chúng bị truy cập từ xa.

  Bạn làm tương tự với vhost còn lại.

  Sau khi cấu hình các vhost xong thì ta phải kích hoạt các vhost này lên, để kích hoạt ta phải liên kết các file vhost này vào thư mục ``sites-enabled``:

  ``# ln -s /etc/nginx/sites-available/website1.dns.info.vn /etc/nginx/sites-enabled/``

  ``# ln -s /etc/nginx/sites-available/website2.dns.info.vn /etc/nginx/sites-enabled/``

  Kiểm tra cấu hình và khởi động lại Nginx với 2 câu lệnh sau:

  ``# nginx -t``: để kiểm tra cấu hình vhost có sai sót gì không

  ``# systemctl reload nginx``: Khởi động lại dịch vụ Nginx để áp dụng cấu hình

  Ta phải đảm bảo rằng thư mục gốc (document root) cho các website đã tồn tại và chứa các file cần thiết:

  ``# mkdir -p /var/www/website1.dns.info.vn``
  
  ``# mkdir -p /var/www/website2.dns.info.vn``

  Thiết lập quyền sở hữu cho đúng:

  ``# chown -R www-data:www-data /var/www/website1.dns.info.vn``
  
  ``# chown -R www-data:www-data /var/www/website2.dns.info.vn``

  Ta kiểm tra bằng cách truy cập vào 2 tên miền ``website1.dns.info.vn`` và ``website2.dns.info.vn`` trên trình duyệt để kiểm tra xem các vhost đã hoạt động đúng chưa.

## 3. Cài đặt Maria DB bản mới nhất

  MariaDB là một hệ quản trị cơ sở dữ liệu mã nguồn mở, được phát triển như một nhánh của MySQL sau khi MySQL được Oracle Corporation mua lại. MariaDB được thiết kế để duy trì khả năng tương thích với MySQL, nhưng với sự tập trung vào cải thiện hiệu suất, bảo mật và tính năng mở rộng.

  * **Bước 1. Cài đặt MariaDB**

    Bạn sử dụng câu lệnh sau để cài đặt MariaDB:

    ``# curl -fsSL https://dlm.mariadb.com/3/MariaDB/mariadb_repo_setup | sudo bash``

    Lệnh này sẽ tải xuống và thực thi script, tự động thêm kho lưu trữ MariaDB vào hệ thống của bạn và cấu hình các tệp cấu hình cần thiết.

    ``# apt install mariadb-server mariadb-client -y``

    **mariadb-server:** Đây là gói phần mềm chứa toàn bộ MariaDB Database Server. Khi cài đặt gói này, bạn sẽ có được một server MariaDB hoàn chỉnh, có thể chạy trên máy chủ của bạn để lưu trữ và quản lý cơ sở dữ liệu.

    **mariadb-client**: Gói phần mềm này chứa công cụ dòng lệnh để tương tác với MariaDB Server. Nó bao gồm công cụ mysql (được đổi tên thành mariadb trong một số hệ thống) dùng để chạy các truy vấn SQL trực tiếp từ dòng lệnh.

    Sau khi cài đặt, bạn cần kiểm tra xem MariaDB đã chạy hay chưa:

    ``# systemctl status mariadb``

    ![](/thuctap/img/mariadb_status.png)

    Nếu chưa thì gõ câu lệnh sau để kích hoạt nó lên:

    ``# systemctl start mariadb``

  * **Bước 2: Cấu hình bảo mật MariaDB**

    MariaDB có một tập hợp các cài đặt bảo mật có thể được cấu hình tự động thông qua một công cụ đi kèm. Công cụ này sẽ giúp bạn thay đổi mật khẩu root, loại bỏ người dùng ẩn danh, cấm đăng nhập root từ xa, và xóa bỏ database test mặc định.

    Các bạn chạy lệnh sau để bắt đầu cấu hình:

    ``# mysql_secure_installation``

    Bạn sẽ được yêu cầu trả lời một số câu hỏi:

      + **Enter current password for root (enter for none)**: Nhấn Enter (mặc định root chưa có mật khẩu).

      + **Switch to unix_socket authentication [Y/n]**: Chọn ``n`` nếu bạn muốn sử dụng mật khẩu để xác thực.

      + **Change the root password? [Y/n]**: Chọn ``Y`` và đặt mật khẩu root mới.

      + **Remove anonymous users? [Y/n]**: Chọn ``Y`` để loại bỏ người dùng ẩn danh.
    
      + **Disallow root login remotely? [Y/n]**: Chọn ``Y`` để cấm đăng nhập root từ xa.
    
      + **Remove test database and access to it? [Y/n]**: Chọn ``Y`` để xóa database test.
    
      + **Reload privilege tables now? [Y/n]**: Chọn ``Y`` để áp dụng các thay đổi.

  * **Bước 3: Đăng nhập vào MariaDB**

    Để truy cập MariaDB và thực hiện các lệnh SQL, ta sử dụng câu lệnh: 

    ``# mysql -u root -p``

    Nhập mật khẩu root mà bạn đã cấu hình trong bước trên để đăng nhập.

  * **Bước 4: Tạo CSDL và người dùng**

    Sau khi đăng nhập vào MariaDB ta gõ các câu lệnh sau để tạo CSDL cho hai website:

        CREATE DATABASE website1_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
        CREATE USER 'website1_user'@'localhost' IDENTIFIED BY 'password1';
        GRANT ALL PRIVILEGES ON website1_db.* TO 'website1_user'@'localhost';
        FLUSH PRIVILEGES;

    Các bạn làm tương tự cho ``website2.dns.info.vn``

    Các lệnh này giúp bạn thiết lập cơ sở dữ liệu, tạo người dùng và cấp quyền cho người dùng đó để quản lý cơ sở dữ liệu.

  * **Bước 5:  Kiểm tra kết nối**
    
    Sau khi tạo xong ta kiểm tra kết nối CSDL từ PHP, đầu tiên ta tạo 1 tệp kiểm tra cho website

    ``# nano /var/www/website1.dns.info.vn/db-test.php``

    Thêm đoạn mã sau vào tệp:

        <?php
        $servername = "localhost";
        $username = "website1_user";
        $password = "password1";
        $dbname = "website1_db";

        // Tạo kết nối
        $conn = new mysqli($servername, $username, $password, $dbname);

        // Kiểm tra kết nối
        if ($conn->connect_error) {
            die("Kết nối thất bại: " . $conn->connect_error);
          }
        echo "Kết nối thành công";
        $conn->close();
        ?>

    Ta thử truy cập vào ``http://website1.dns.info.vn/db-test.php`` để kiểm tra kết quả.

    ![](/thuctap/img/mariadb_check.png)

    Ta làm tương tự với website còn lại

## 4. Cài đặt phpMyadmin

**phpMyAdmin** là một công cụ quản lý cơ sở dữ liệu MySQL và MariaDB qua giao diện web. Đây là một trong những công cụ phổ biến nhất để quản lý các cơ sở dữ liệu và thực hiện các tác vụ liên quan đến cơ sở dữ liệu mà không cần sử dụng dòng lệnh.

Ta sẽ cài đặt phpMyAdmin và các mô-dun php bổ sung bằng lệnh sau:

``# apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y``

* **php-mbstring**: Dùng để quản lý các chuỗi không phải ASCII và chuyển đổi các chuỗi thành các bảng mã hoá khác nhau.

* **php-zi**p: Hỗ trợ tải các file có đuôi .zip lên phpMyAdmin

* **php-gd**: Hỗ trợ thư viện đồ hoạ GD

* **php-json**: Cung cấp php hỗ trợ tuần tự hoá json

* **php-curl**: Cho phép php tương tác với các loại máy chủ khác nhau bằng các giao thức khác nhau

Khi cài đặt, hệ thống sẽ yêu cầu bạn chọn máy chủ web mà phpMyAdmin sẽ sử dụng. Chọn ``apache2``, sau đó ta sẽ cấu hình ``Nginx`` thủ công sau.

  ![](/thuctap/img/phpMyadmin_apache.png)

Kế đến, bạn sẽ được hỏi có muốn cài đặt và cấu hình cơ sở dữ liệu cho phpMyAdmin không. Chọn ``Yes``, rồi nhập mật khẩu cho tài khoản quản trị viên phpMyAdmin.

  ![](/thuctap/img/phpMyadmin_select.png)

  ![](/thuctap/img/phpMyadmin_password.png)

  ![](/thuctap/img/phpMyadmin_password_confirm.png)

Kích hoạt các tiện ích PHP cần thiết:

``# phpenmod mbstring``

```# phpenmod zip```

Tạo một liên kết tượng trưng (symbolic link) để phpMyAdmin có thể được truy cập từ Nginx:

``# ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin``

Sau đó, ta sẽ cấu hình Nginx để sử dụng phpMyAdmin với phiên bản PHP cụ thể, mở tệp cấu hình Nginx cho trang web website1.dns.info.vn

``# nano /etc/nginx/sites-available/website1.dns.info.vn``

Ta thêm phần cấu hình dưới đây để phpMyadmin sử dụng PHP 8.2:


    server {
    listen 80;
    server_name website1.dns.info.vn;
    root /var/www/website1.dns.info.vn;
    index index.php index.html index.htm;

    # Xử lý các yêu cầu đến root của website1
    location / {
        try_files $uri $uri/ =404;
    }

    # Xử lý các yêu cầu PHP cho website1 bằng PHP 8.2
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    # Cấm truy cập các tệp .ht
    location ~ /\.ht {
        deny all;
    }

    # Cấu hình cho phpMyAdmin
    location /phpmyadmin {
        root /usr/share;
        index index.php;

        # Xử lý các yêu cầu PHP cho phpMyAdmin bằng PHP 7.4
        location ~ ^/phpmyadmin/(.+\.php)$ {
            try_files $uri =404;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $request_filename;
            include fastcgi_params;
        }

        # Xử lý các tệp tĩnh của phpMyAdmin
        location ~* ^/phpmyadmin/(.+\.(jpg|jpeg|gif|css|png|js|ico|html|xml|txt))$ {
            try_files $uri =404;
        }
    }
  }


Ta làm tương tự với website ``website2.dns.info.vn``, tuy nhiên ta cần phải thay đổi ``fastcgi_pass`` để sử dụng PHP 7.4

Ta kiểm tra và khởi động lại Nginx

## 5. Certbot

**Certbot** là một công cụ mã nguồn mở được phát triển bởi Electronic Frontier Foundation (EFF) giúp tự động hóa việc cấp và gia hạn chứng chỉ SSL/TLS cho các trang web. Cung cấp chứng chỉ SSL/TLS miễn phí từ Let's Encrypt, Certbot giúp bảo mật trang web bằng cách mã hóa kết nối giữa máy chủ và trình duyệt của người dùng. Nó có thể tự động cấu hình chứng chỉ cho nhiều máy chủ web, bao gồm Apache và Nginx, và tự động gia hạn chứng chỉ khi chúng gần hết hạn.

Để cài đặt Certbot trên Ubuntu 20.04 và cấu hình nó để cấp chứng chỉ SSL/TLS cho trang web của bạn, bạn có thể làm theo các bước dưới đây:

  * **Cập nhật danh sách gói và cài đặt các gói cần thiết:**

        # apt update -y
        # apt install certbot python3-certbot-nginx -y

  * **Cấu hình chứng chỉ SSL/TLS cho NGINX:**

    Nếu bạn đang sử dụng NGINX, bạn có thể yêu cầu Certbot tự động cấu hình chứng chỉ SSL/TLS cho bạn bằng cách sử dụng lệnh sau:

        # certbot --nginx -d website1.dns.info.vn -d website2.dns.info.vn

    Trong lệnh trên, thay ``website1.dns.info.vn`` và`` website2.dns.info.vn`` bằng tên miền của bạn. Nếu bạn có nhiều tên miền hoặc subdomain khác, hãy thêm chúng vào danh sách các tham số ``-d``.

    Khi chạy lệnh, bạn sẽ được yêu cầu cung cấp địa chỉ email và chấp nhận các điều khoản sử dụng. Certbot sẽ tự động cấu hình NGINX để sử dụng chứng chỉ SSL/TLS và thực hiện kiểm tra để xác nhận rằng chứng chỉ đã được cài đặt đúng.    

    Sau khi cài đặt thành công SSL thông qua Certbot, đường đẫn lưu file chứng chỉ của website sẽ nằm tại đường dẫn tương ứng.

    ![](/thuctap/img/certbot_key.png)

  * **Gia hạn SSL/TLS:**

    Vì hứng chỉ SSL/TLS do certbot tạo chỉ có hiệu lực trong 90 ngày, do đó bạn có thể thiết lập cronjob  để chứng chỉ tự động gia hạn nếu như hết hạn.

        # crontab -e

    Thêm dòng này để vào file crontab để chạy lệnh gia hạn chứng chỉ vào lúc 2 giờ sáng.

        0 2 * * * /usr/bin/certbot renew --quiet    


  * **Kiểm tra chứng chỉ sau khi cài đặt**

    * Cách 1: Kiểm tra từ trình duyệt

      Bạn có thể truy cập website của mình ở trình duyệt và click vào biểu tượng ổ khóa như hình bên dưới kiểm tra. Tại đây sẽ hiển thị website đang sử dụng chứng chỉ của hãng nào, đồng thời cũng ghi rõ ngày cấp và ngày hết hạn.
# END