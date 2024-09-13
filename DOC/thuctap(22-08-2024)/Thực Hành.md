# LEMP Stack trên Ubuntu 20.04 và WordPress


# Mục lục
- [LEMP Stack trên Ubuntu 20.04 và WordPress](#lemp-stack-trên-ubuntu-2004-và-wordpress)
- [Mục lục](#mục-lục)
- [I. Chuẩn bị](#i-chuẩn-bị)
  - [Thiết lập sủ dụng SSH Key trên Linux](#thiết-lập-sủ-dụng-ssh-key-trên-linux)
  - [Thiết lập sủ dụng SSH Key trên Window](#thiết-lập-sủ-dụng-ssh-key-trên-window)
  - [Đổi port SSH sang 2024](#đổi-port-ssh-sang-2024)
- [II. Cài đặt LEMP](#ii-cài-đặt-lemp)
  - [1. Cài đặt Nginx](#1-cài-đặt-nginx)
  - [2. PHP-FPM pools](#2-php-fpm-pools)
  - [3. Cài đặt Maria DB bản mới nhất](#3-cài-đặt-maria-db-bản-mới-nhất)
  - [4. Cài đặt phpMyadmin](#4-cài-đặt-phpmyadmin)
  - [5. Certbot](#5-certbot)
  - [6. Cài dịch vụ Redis Cache](#6-cài-dịch-vụ-redis-cache)
- [III. Cài đặt website WordPress](#iii-cài-đặt-website-wordpress)
  - [1. Cài đặt WordPress](#1-cài-đặt-wordpress)
  - [2. Cấu hình WordPress](#2-cấu-hình-wordpress)
  - [3. Cài theme WordPress](#3-cài-theme-wordpress)
    - [Cách 1. Cài Đặt Theme Qua Bảng Điều Khiển WordPress\*\*](#cách-1-cài-đặt-theme-qua-bảng-điều-khiển-wordpress)
    - [Cách 2. Cài đặt Theme qua Tập Tin ZIP](#cách-2-cài-đặt-theme-qua-tập-tin-zip)
  - [4. Cài đặt SMTP và cấu hình SMTP Gmail](#4-cài-đặt-smtp-và-cấu-hình-smtp-gmail)
- [END](#end)

# I. Chuẩn bị

Một VPS Ubuntu có địa chỉ IP: ``103.110.85.87``

## Thiết lập sủ dụng SSH Key trên Linux

 Để tạo SSH Key ta nhập lệnh sau: ``ssh-keygen -t rsa`` để tạo chuổi Public key và Private key ở máy khách.

 ![](/img/VPS_SSHKey.png)

Trong thông báo bạn sẽ thấy 2 dòng:

**Your identification has been saved in ``name_key``**: Đây là thông báo cho bạn biết rằng khóa riêng tư (Private key) của bạn đã được lưu trong tệp.

**Your Public key has been saved in ``name_key.pub``**: Đây là thông báo cho bạn biết rằng khóa công khai (Public key) đã được lưu trong tệp

Thông thường khi bạn nhập lệnh tạo SSH Key thì Public key và Private key lưu tại thư mục ``.ssh`` mà bạn nhập lệnh, ta dùng lệnh ``ls -al`` để in các tệp có trong thư mục ra.

![](/img/VPS_2Key.png)

Tiếp theo ta thêm Public key lên VPS. Bạn hãy ssh vào VPS với thông tin passwd root và thực hiện nhập tuần tự các lệnh sau.

    # mkdir ~/.ssh                      Tạo thư mục .ssh 
    # chmod 700 ~/.ssh                  Đặt quyền truy cập cho thư mục .ssh thành 700.
    # touch ~/.ssh/authorized_keys      Tạo một tệp rỗng có tên authorized_keys trong thư mục .ssh
    # chmod 600 ~/.ssh/authorized_keys  Đặt quyền truy cập cho tệp authorized_keys thành 600

Những lệnh này thiết lập môi trường bảo mật cho SSH bằng cách tạo thư mục và tệp cần thiết và cấu hình các quyền truy cập phù hợp. Điều này giúp bảo vệ dữ liệu xác thực SSH của bạn khỏi các truy cập trái phép và đảm bảo rằng chỉ có người dùng được phép mới có thể kết nối qua SSH.


* **Copy Public key bằng cách thủ công**

  Trên con máy có chứa Public key của bạn, bạn mở terminal và chạy lệnh ``cat`` để hiển thị nội dung của khoá và copy nó.

  ![](/img/VPS_CatPub.png)

  Bạn SSH tới VPS như bằng cách sử dụng lệnh: ``# ssh user@ip_server``

  Trong đó: 
  
    * ``user``: Tên người dùng trên máy chủ từ xa mà bạn muốn đăng nhập.

    * ``ip_server``: Địa chỉ IP hoặc tên miền của máy chủ từ xa mà bạn muốn kết nối đến.
  
  Sau đó ta sử dụng lệnh: ``# nano ~/.ssh/authorized_keys`` để mở thư mục ``authorized_keys`` và dán key đã copy vào.

  ![](/img/VPS_SSHCopy.png)

  Để sử dụng SSH key, ta mở Terminal lên và sử dụng lệnh sau để SSH:

  ``# ssh -i duong_dan_chua_Private_key root@ip_may_chu -p port_SSH``

  ![](/img/VPS_SSH_Succes.png)

  Sau khi đã SSH key thành công bạn có thể tắt cho phép SSH bằng Passwd đi để tránh do passwd và brute force attack nhé. Để tắt đăng nhập ssh bằng passwd bạn thực hiện như sau. Bạn mở file ``/etc/ssh/sshd_config`` sau đó tìm đến dòng ``PasswordAuthentication Yes`` bạn chuyển thành ``PasswordAuthentication no``

  ![](/img/VPS_yestono.png)

  Sau khi lưu xong bạn đừng quên khởi động lại dịch vụ ssh.

  ``# systemctl restart sshd``

## Thiết lập sủ dụng SSH Key trên Window

Ngoài cách sử dụng command line trên Linux ngoài ra ta còn có cách khác là sử dụng phần mềm Putty để tạo SSH key và sử dụng SSH key đó để đăng nhập vào VPS.

* **Tạo SSH key bằng PuttyGen**

  ![](/img/VPS_Putty_Gene.png)


  ![](/img/VPS_Putty_Click.png)

  ![](/img/VPS_Putty_SaveKey.png)

* **Sử dụng SSH Key trên Putty**

  Bạn mở PuTTY lên sau đó click vào SSH => Auth. Tiếp đến bạn clck vào Browse để tìm đến file Private key đã tạo và lưu.. Khi đã trỏ được đến file Private và bạn thực hiện SSH thì bạn sẽ nhận được yêu cầu nhập vào Passphrase, bạn hãy nhập Passphrase để hoàn tất bước SSH nhé.

  ![](/img/VPS_Putty_Connect.png)

## Đổi port SSH sang 2024

Mở tệp cấu hình SSH (``/etc/ssh/sshd_config``) bằng trình soạn thảo văn bản:

``# nano /etc/ssh/sshd_config``

Tìm dòng có nội dung ``#Port 22``. Bỏ dấu ``#`` và thay đổi số 22 thành 2024:

![](/img/VPS_Port2024.png)

Mở cổng 2024 trên tường lửa:

``# ufw allow 2024/tcp``

``# ufw enable``

Khởi động lại dịch vụ SSH để áp dụng các thay đổi:

``# systemctl restart sshd``


# II. Cài đặt LEMP

## 1. Cài đặt Nginx

  Nginx là một máy chủ web phổ biến được sử dụng để phục vụ các trang web, nhưng nó còn có khả năng hoạt động như một máy chủ proxy ngược (reverse proxy), cân bằng tải (load balancer), và proxy email (IMAP/POP3)

  * **Bước 1: Cài đặt Nginx**

    Một điều vô cùng quan trọng trước khi cài một phần mềm mới, bạn phải cập nhật danh sách repository của mình.

    ``# apt update -y``

    Sau khi hoàn thành cập nhật thì bạn gõ lệnh:

    ``# apt install nginx -y``

    Tiếp theo bạn hãy kiểm tra xem nginx đã cài đặt chưa bằng lệnh:

    ``# nginx -v``

    Nó sẽ trả ra kết quả như sau:

    ![](/img/nginx_v_2.png)

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

    ![](/img/Nginx_success_v2.png)

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

    ![](/img/VPS_PHP_Pool_8_2.png)

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
        root /var/www/html;
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
        root /var/www/html;
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

    ![](/img/mariadb_status.png)

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

          CREATE DATABASE wordpress_db;

          # Các bạn có thể thay đổi user và password của database
          CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'your_password'; 
          
          
          GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
          FLUSH PRIVILEGES;
          EXIT;


    Các lệnh này giúp bạn thiết lập cơ sở dữ liệu, tạo người dùng và cấp quyền cho người dùng đó để quản lý cơ sở dữ liệu.

  * **Bước 5:  Kiểm tra kết nối**
    
    Sau khi tạo xong ta kiểm tra kết nối CSDL từ PHP, đầu tiên ta tạo 1 tệp kiểm tra cho website

    ``# nano /var/www/website1.dns.info.vn/db-test.php``

    Thêm đoạn mã sau vào tệp:

        <?php
        $servername = "localhost";
        $username = "wordpress_user";
        $password = "your_password";
        $dbname = "wordpress_db";

        // Tạo kết nối
        $conn = new mysqli($servername, $username, $password, $dbname);

        // Kiểm tra kết nối
        if ($conn->connect_error) {
            die("Kết nối thất bại: " . $conn->connect_error);
        }
        echo "Kết nối thành công!";
        $conn->close();
        ?>
    Ta thử truy cập vào ``http://website1.dns.info.vn/db-test.php`` để kiểm tra kết quả.

    ![](/img/mariadb_check.png)

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

  ![](/img/phpMyadmin_apache.png)

Kế đến, bạn sẽ được hỏi có muốn cài đặt và cấu hình cơ sở dữ liệu cho phpMyAdmin không. Chọn ``Yes``, rồi nhập mật khẩu cho tài khoản quản trị viên phpMyAdmin.

  ![](/img/phpMyadmin_select.png)

  ![](/img/phpMyadmin_password.png)

  ![](/img/phpMyadmin_password_confirm.png)

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
    root /var/www/html;
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

    ![](/img/certbot_key.png)

  * **Gia hạn SSL/TLS:**

    Vì hứng chỉ SSL/TLS do certbot tạo chỉ có hiệu lực trong 90 ngày, do đó bạn có thể thiết lập cronjob  để chứng chỉ tự động gia hạn nếu như hết hạn.

        # crontab -e

    Thêm dòng này để vào file crontab để chạy lệnh gia hạn chứng chỉ vào lúc 2 giờ sáng.

        0 2 * * * /usr/bin/certbot renew --quiet    


Bạn có thể kiểm tra chứng chỉ SSL của trang web của mình bằng cách nhấn hình chìa khoá ngay cạnh tên miền của trang web hoặc kiểm tra chứng chỉ SSL của mình tại trang web **https://www.sslshopper.com/**

![](/img/certbot_check.png)

## 6. Cài dịch vụ Redis Cache

Redis (**Remote Dictionary Server**) là một dịch vụ cơ sở dữ liệu in-memory, mã nguồn mở, đóng vai trò như một cache, message broker, và data store. Nó được sử dụng rộng rãi nhờ vào tốc độ xử lý cao, tính linh hoạt và khả năng mở rộng tốt.

* **Bước 1. Cài đặt Redis Server**

  Thông thường thì các gói Redis sẽ có sẵn trong kho APT mặc định của hệ điều hành Ubuntu. Để cài đặt Redis trên VPS Ubuntu bạn hãy nhập lệnh sau:

        # apt update -y
        # apt install redis-server -y

  Sau đó, hãy cho phép Redis khởi động lại cùng với hệ thống khi hệ thống khởi động.

        # systemctl enable redis-server

* **Bước 2. Cấu hình Redis**

  Bạn muốn thực hiện chỉnh sửa tệp cấu hình của REdis thì thông thường sau khi cài đặt xong thì tệp cấu hình của redis nó nằm ở đường dẫn : /etc/redis/redis.conf

        #  nano /etc/redis/redis.conf

  Giả sử bạn muốn Redis lắng nghe trên địa chỉ IP của VPS của bạn thì bạn hãy chỉnh sửa dòng **bind 127.0.0.1 ::1** thành **bind IP_VPS_cua_ban**

  ![](/img/Redis_Bind.png)

  Tiếp theo bạn NÊN bật bảo mật bằng cách yêu cầu mật khẩu.

  ![](/img/Redis_foobared.png) 

  Ta khởi động lại dịch vụ Redis để áp dụng cấu hình.

        # systemctl restart redis-server 

* **Bước 3: Cấu hình tường lửa (Firewall)**

  Nếu bạn có sử dụng tường lửa trên VPS, hãy đảm bảo rằng cổng Redis (mặc định là 6379) được mở cho các IP mà bạn muốn cho phép truy cập

  Mở cổng 6379 cho địa chỉ IP cụ thể hoặc cho mạng ngoài

        # ufw allow from 127.0.0.1 to any port 6379 (Cho localhost )

        # ufw allow from IP_VPS_cua_ban to any port 6379 (cho một mạng cụ thể)

        # ufw status

* **Bước 4: Kiểm tra kết nối**

  Nếu bạn đang trên cùng một máy chủ nơi Redis được cài đặt, bạn có thể sử dụng redis-cli để kiểm tra kết nối:

        # redis-cli (Nếu bạn không bật bảo mật yêu cầu mật khẩu)

        # redis-cli -h IP_VPS_cua_ban -p 6379 -a mat_khau_redis (Nếu bạn đã cấu hình bảo mật yêu cầu mật khẩu)

  Khi kết nối thành công, bạn sẽ thấy dấu nhắc của Redis (127.0.0.1:6379>). Từ đây, bạn có thể thử một số lệnh để kiểm tra:

        # PING

  Redis sẽ trả về PONG nếu kết nối thành công.

  ![](/img/Redis_ping.png)

# III. Cài đặt website WordPress

WordPress là một phần mềm nguồn mở dùng để tạo và quản lý nội dung website. Nó hoạt động như một hệ thống quản lý nội dung (CMS) cho phép người dùng tạo, chỉnh sửa, đăng và quản lý các bài viết, trang web một cách đơn giản thông qua giao diện trực quan.

Điểm mạnh chính của WordPress là nguồn mã nguồn mở miễn phí, cho phép bất kỳ ai cũng có thể sử dụng, chỉnh sửa và phát triển. Nó cũng có hệ sinh thái plugin và giao diện (theme) phong phú, tùy biến dễ dàng theo nhu cầu. Cộng đồng người dùng và nhà phát triển rất lớn, luôn cập nhật các tính năng mới.

## 1. Cài đặt WordPress

  Mặc định thư mục chứa mã nguồn của website sẽ nằm ở đường dẫn: **/var/www/html**. Bạn di chuyển vào thư mục này và thực hiện tiếp các bước sau.

      # cd /var/www/html
      # wget https://wordpress.org/latest.zip (Tải WordPress về)
  
  Sau khi tải về các bạn dùng các công cụ giải nén nó ra, tại đây mình dùng unzip

      # unzip latest.zip

  Với mã nguồn download từ trang chủ, khi giải nén sẽ có sẵn một thư mục là WordPress. Vì vậy cần di chuyển mã nguồn ra document root, và phân quyền lại.

      # mv wordpress/* .
      # chown -R www-data:www-data /var/www/html
      # chmod -R 755 /var/www/html

  
  Xóa các file không cần thiết:

      # rm -rf wordpress latest.zip


## 2. Cấu hình WordPress

  Sau khi cài đặt thành công các bạn vào tên miền của các bạn để cấu hình WordPress

  ![](/img/WordPress_select_tv.png)

  ![](/img/WordPress_begin_config.png)

  Tại đây các bạn nhập thông tin database đã tạo để áp dụng vào WordPress. Về phần tiền tố bản dữ liệu nếu các bạn chỉ có 1 trang WordPress thì các bạn có thể bỏ qua, còn nếu các bạn có 2 trang web trở lên mà lại dùng chung 1 database thì các bạn khai bao thứ tự cho dễ quản lí

  ![](/img/WordPress_Database.png)

  ![](/img/WordPress_end_config.png)

  ![](/img/WordPress_info.png)

## 3. Cài theme WordPress

  WordPress cho phép bạn thay đổi giao diện của trang web bằng cách cài đặt các theme khác nhau. Có rất nhiều cách để cài đặt theme cho Wordpress, sau đây mình sẽ hướng dẫn các cách thông dụng để cài đặt theme cho Wordpress của bạn

### Cách 1. Cài Đặt Theme Qua Bảng Điều Khiển WordPress**

  * **Bước 1: Đăng Nhập Vào Bảng Điều Khiển WordPress**
    + Mở trình duyệt và truy cập vào trang đăng nhập của WordPress (thường là http://yourdomain.com/wp-admin).

    + Nhập tên đăng nhập và mật khẩu của bạn để truy cập vào bảng điều khiển WordPress.
      
    ![](/img/WordPress_login.png)

  * **Bước 2: Truy Cập Phần Giao Diện**
  
    + Trong thanh điều hướng bên trái, chọn “Giao diện” (Appearance).
  
    + Nhấp vào “Themes” (Giao diện) để mở danh sách các theme hiện tại.
    
    ![](/img/WordPress_Appearance.png)
  * **Bước 3: Thêm Mới Theme**
  
    + Nhấp vào nút “Thêm mới” (Add New Theme) ở phía trên cùng của trang.
    
    ![](/img/WordPress_AddTheme.png)
  * **Bước 4: Tìm Kiếm và Cài Đặt Theme**
    
    + Search Themes: Bạn có thể sử dụng thanh tìm kiếm để tìm theme theo tên, hoặc duyệt qua các theme phổ biến, mới nhất hoặc được đề xuất.
    
    + Cài Đặt Theme: Khi bạn tìm thấy theme bạn muốn cài đặt, di chuyển chuột qua hình thu nhỏ của theme và nhấp vào nút “Install” (Cài đặt).
  
    ![](/img/WordPress_Install.png)
  * **Bước 5: Kích Hoạt Theme**
    + Sau khi theme đã được cài đặt, nhấp vào “Kích hoạt” (Activate) để làm cho theme đó trở thành giao diện chính của trang web.
  
    ![](/img/WordPress_Activated.png)

### Cách 2. Cài đặt Theme qua Tập Tin ZIP

  * **Bước 1: Tải Tập Tin ZIP của Theme:**
  
    + Đầu tiên, bạn cần tải tập tin ZIP của theme mà bạn muốn cài đặt từ trang web cung cấp theme. Tại đây mình sẽ tải hai theme là **https://tool.dotrungquan.info/wordpress/theme/Soledad-v8.1.9.zip** và **https://tool.dotrungquan.info/wordpress/theme/flatsome-3.19.3.zip**

  * **Bước 2: Đăng Nhập Vào Bảng Điều Khiển WordPress:**
    
    ![](/img/WordPress_login.png)
  
  * **Bước 3: Truy Cập Phần Giao Diện:**

    ![](/img/WordPress_Appearance.png)

  * **Bước 4: Tải Lên Theme (Upload Theme)**

    + Ở phía trên của trang, nhấn vào nút "Tải lên giao diện" (Upload Theme).

    ![](/img/WordPress_Upload.png)


  * **Bước 5 Chọn Tập Tin ZIP:**

    + Nhấn vào nút "Chọn tệp" (Choose File), sau đó chọn tập tin ZIP của theme mà bạn đã tải về trước đó.

    ![](/img/WordPress_ChooseFile.png)

  * **Bước 6: Cài Đặt:**

    + Trước khi chọn tập tin, các bạn giải nén file theme mà các bạn tải về. Tuỳ vào mỗi theme sẽ có cách cài đặt khác nhau, các bạn nên lên trang chủ mà theme các bạn tải về để xem hướng dẫn cài theme thông qua file zip trên WordPress

    + Sau khi chọn tập tin, nhấn vào nút "Cài đặt ngay" (Install Now) để bắt đầu quá trình cài đặt.

    ![](/img/WordPress_InstallZip.png)

    ![](/)

  * **Bước 7: Kích Hoạt Theme:**

    + Sau khi cài đặt thành công, bạn sẽ thấy thông báo thành công với các lựa chọn như "Kích hoạt" (Activate) hoặc "Xem trước trực tiếp" (Live Preview). Nhấn vào "Kích hoạt" để bắt đầu sử dụng theme mới.
  
    ![](/img/WordPress_SuccessTheme.png)

    Website 1:

    ![](/img/WordPress_Soleadad.png)

    Website 2:

    ![](/img/WordPress_Floatsome.png)

## 4. Cài đặt SMTP và cấu hình SMTP Gmail

**SMTP là gì?**

  SMTP (Simple Mail Transfer Protocol) là giao thức truyền tải thư điện tử qua mạng Internet. Trong bài viết này, chúng ta sẽ tìm hiểu cách kết nối SMTP Gmail với website WordPress để cải thiện khả năng gửi và nhận thư tín. Bằng cách này, bạn có thể tự động thông báo về các hoạt động quan trọng trên trang web của mình, như thao tác đặt hàng từ khách hàng.

**Cài đặt Plugin SMTP**

  Trên WordPress đã có nhiều tùy chọn plugin SMTP phổ biến và dễ sử dụng như **WP Mail SMTP**, **Easy WP SMTP**, và** Post SMTP**. Những plugin này hỗ trợ việc định cấu hình máy chủ SMTP, giúp cải thiện độ tin cậy khi gửi email từ trang web của bạn. Chỉ cần cài đặt và cấu hình theo hướng dẫn, bạn có thể dễ dàng thiết lập email qua SMTP mà không cần kiến thức sâu về kỹ thuật.

  Trong bài làm này mình sẽ cài đặt Plugin **Easy WP SMTP** cho cả hai trang web của mình

  **Bước 1: Cài đặt Plugin:**

  + Các bạn vào phần **Plugins** > **Add New**. Trong ô tìm kiếm, gõ “Easy WP SMTP”.

  ![](/img/WordPress_Plugins.png)

  + Khi thấy plugin Easy WP SMTP, nhấn **Install Now**. Sau khi cài đặt xong, nhấn **Activate** để kích hoạt plugin.

  ![](/img/WordPress_Install_SMTP.png)

  ![](/img/WordPress_Activated_SMTP.png)

**Cấu hình SMTP Gmail**

Trước khi ta vào cấu hình SMTP Gmail ta cần lấy mật khẩu ứng dụng Gmail để đảm bảo rằng kết nối được thực hiện một cách an toàn mà không cần phải tiết lộ mật khẩu chính của tài khoản, đồng thời giữ cho tài khoản được bảo mật tốt hơn.

  **Lấy mật khẩu ứng dụng Gmail**

  Đầu tiên bạn đăng nhập vào tài khoản Gmail của bạn. Truy cập vào trang quản lý tài khoản bằng cách điều hướng đến Goolge tài khoản >> Truy cập vào Tài khoản Google

  ![](/img/Google_login.png)

  Tiếp theo bạn chọn mục **Bảo mật** và **kích hoạt xác minh hai bước** (2-Step Verification) nếu chưa bạn cần phải thực hiện xác minh trước đó.

  ![](/img/Google_2step.png)

  Sau khi hoàn tất xác minh hai bước, các bạn hãy tới liên kết này để tạo mật khẩu ứng dụng của các bạn: **https://myaccount.google.com/apppasswords**

  Tại đây các bạn đặt tên mật khẩu ứng dụng và trang sẽ tự động tạo ngẫu nhiên mật khẩu ứng dụng của bạn

  ![](/img/Google_SMTPPASS.png)

  ![](/img/Google_hiddenpass.png)

  **Cấu hình Plugin SMTP**

  Bạn vào phần plugin WP SMPT bạn kéo xuống đến phần **Mailer Settings** và bạn chon phần **Other SMTP**

  ![](/img/WPSMTP_Mailer.png)

  **Trong phần Other SMTP**, phần này sẽ yêu cầu nhập các thông tin sau đây:

  ![](/img/WPSMTP_OtherSMTP.png)

  + **SMTP Host**: smtp.gmail.com — Đây là địa chỉ máy chủ SMTP của Gmail.

  + **Type of Encryption**: Tùy chọn mã hóa, ví dụ:

    + SSL: Nếu bạn chọn SSL, sử dụng cổng 465.
    + TLS: Nếu bạn chọn TLS, sử dụng cổng 587.

  + **SMTP Port**:

    + 465 nếu sử dụng mã hóa SSL.
    
    + 587 nếu sử dụng mã hóa TLS.

  + **SMTP Username**: Đây là địa chỉ email Gmail của bạn. (Ví dụ: your-email@gmail.com)

  + **SMTP Password**: Mật khẩu ứng dụng Gmail mà bạn đã tạo ở bước trước (không phải mật khẩu chính của tài khoản Gmail).

  Tiếp đến là phần **General Settings**

  ![](/img/WPSMTP_General.png)

  + **From Email Address:**

    Nhập địa chỉ email mà bạn sử dụng để tạo mật khẩu ứng dụng. Đây sẽ là địa chỉ email hiển thị trên các email gửi đi từ trang web của bạn.

  + **From Name:**

    Nhập tên bạn muốn hiển thị trên email gửi đi. Đây là tên mà người nhận sẽ thấy trong phần "Tên người gửi" của email. Ví dụ: bạn có thể nhập tên công ty của bạn hoặc tên của website.

Sau khi cấu hình xong các bạn hãy nhấn Save Setting để lưu cấu hình. Sau đó các bạn vào mục **Send a text** rồi click vào ô **Send Test Email** để gửi một email kiểm tra cấu hình đã được chưa

  ![](/img/WPSMTP_Sendtest.png)

Và đây là email sau khi thành công.

  ![](/img/WPSMTP_email.png)

# END