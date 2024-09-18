# Kết nối Redis với Wordpress

# Mục lục

- [Kết nối Redis với Wordpress](#kết-nối-redis-với-wordpress)
- [Mục lục](#mục-lục)
- [I. Giới thiệu Redis Cache](#i-giới-thiệu-redis-cache)
- [II. Cài đặt và cấu hình](#ii-cài-đặt-và-cấu-hình)
  - [1. Cài đặt Redis](#1-cài-đặt-redis)
    - [a. Trên WordPress](#a-trên-wordpress)
    - [b. Trên Linux](#b-trên-linux)
  - [2. Cấu hình Redis](#2-cấu-hình-redis)
    - [a. Cấu hình quyền truy cập từ xa](#a-cấu-hình-quyền-truy-cập-từ-xa)
    - [b. Cấu hình Unix Socket Redis](#b-cấu-hình-unix-socket-redis)
- [END](#end)

# I. Giới thiệu Redis Cache

Redis Cache hay Redis là một hệ thống lưu trữ dữ liệu có cấu trúc trên bộ nhớ (RAM). Nó cung cấp một cấu trúc dữ liệu key-value linh hoạt và khả năng lưu trữ dữ liệu trên bộ nhớ chính, giúp tăng tốc độ truy xuất dữ liệu.

Redis thường được sử dụng như một cache hoặc bộ nhớ đệm (cache or caching layer) trong các ứng dụng web để giảm thời gian truy cập vào cơ sở dữ liệu chậm.


* **Ưu điểm:**

  + **Tốc độ nhanh**: Redis lưu trữ dữ liệu trong bộ nhớ (RAM) thay vì lưu trữ trên ổ cứng, giúp truy cập dữ liệu nhanh chóng với độ trễ thấp, rất lý tưởng cho việc cache dữ liệu.
  
  + **Hỗ trợ đa dạng kiểu dữ liệu**: Redis hỗ trợ nhiều kiểu dữ liệu như strings, lists, sets, sorted sets, hashes, bitmaps, hyperloglogs, và streams, giúp dễ dàng lưu trữ và thao tác các loại dữ liệu khác nhau.
  
  + **Khả năng mở rộng**: Redis hỗ trợ clustering và replication (nhân bản) giúp cải thiện khả năng mở rộng và tính khả dụng (high availability) của hệ thống.

  + **Dễ cài đặt và sử dụng**: Redis có giao diện đơn giản, dễ hiểu, và việc cấu hình không quá phức tạp, giúp triển khai nhanh chóng.

* **Nhược điểm:**

  + **Bị giới hạn bởi dung lượng RAM**: Redis lưu trữ dữ liệu trên RAM, nên nếu dữ liệu quá lớn, sẽ cần một lượng RAM lớn, gây tốn kém và không khả thi với các tập dữ liệu khổng lồ.
  
  + **Không phù hợp cho lưu trữ dữ liệu lâu dài**: Redis phù hợp cho việc cache, nhưng không lý tưởng cho việc lưu trữ dữ liệu lâu dài vì RAM đắt hơn ổ cứng và dữ liệu có thể mất khi server bị tắt hoặc khởi động lại (trừ khi dùng snapshot hoặc AOF).
  
  + **Cần cấu hình clustering phức tạp**: Redis có tính năng clustering, nhưng khi cần mở rộng quy mô lớn, việc cấu hình và quản lý các node trong cluster trở nên phức tạp.

  + **Không hỗ trợ SQL**: Redis không hỗ trợ các câu truy vấn SQL phức tạp như các cơ sở dữ liệu truyền thống (SQL databases), nên khó khăn hơn cho những ai quen làm việc với SQL.

  + **Tính năng giao dịch hạn chế**: Mặc dù Redis hỗ trợ giao dịch (transactions), nhưng nó không có tính năng phức tạp như khóa bảng (table locking) hay rollbacks, điều này có thể hạn chế trong một số trường hợp sử dụng.

# II. Cài đặt và cấu hình

## 1. Cài đặt Redis

### a. Trên WordPress

Trên WordPress muốn cài đặt Redis Cache cho website ta có thể cài plugin của nó. Hiện nay có nhiều plugin của Redis Cache trong số đó thì plugin **Redis Object Cache** là phổ biến nhất. Bạn có thể cài đặt plugin này trực tiếp từ bảng điều khiển WordPress hoặc tải về từ thư viện plugin trên WordPress.org.

* **Bước 1: Vào trang bảng điều kiển WordPress của website của bạn.**

Bạn đãng nhập vào trang bảng điều kiển WordPress của website mà bạn đang sở hữu

![](/img/WordPress_login.png)

* **Bước 2: Cài đặt Redis Object Cache**

Bạn truy cập vào phần **Plugins(1)** -> **Add New Plugin(2)** -> **Nhấp vào ô Search và gõ "Redis Object Cache(3)"** -> **Và nhấp vào ô Install Now của Redis Object Cache(4)**

![](/img/WordPress_Plugin_Redis.png)

Sau khi tải xong các bạn nhấn vào ô Activate để kích hoạt plugin

![](/img/WordPress_Activated_Redis.png)

* **Bước 3: Khởi động Redis Object Cache**

Sau khi đã kích hoạt plugin Redis Object Cache thì các bạn vào phần Settings -> Redis để vào trang plugin của Redis.

![](/img/WordPress_Setting_Redis.png)

* **Bước 4. Khởi động Redis**

Sau khi các bạn đã vào trang plugin của Redis các bạn nhấp vào ô ``Enable Object Cache`` để kích hoạt Redis lên

![](/img/WordPress_Redis_Enable.png)

Đây là sau khi kích hoạt thành công

![](/img/WordPress_Redis_Succ.png)

### b. Trên Linux

Thông thường thì các gói Redis sẽ có sẵn trong kho mặc định của hệ điều hành Linux. Để cài đặt Redis các bạn hãy nhập lệnh sau:

      # apt update -y
      # apt install redis-server -y

Sau đó, hãy cho phép Redis khởi động lại cùng với hệ thống khi hệ thống khởi động.

      # systemctl enable redis-server

Kiểm tra xem Redis đã khởi động chưa:

      # systemctl status redis

## 2. Cấu hình Redis

### a. Cấu hình quyền truy cập từ xa

Theo mặc định, Redis không cho phép kết nối từ xa. Bạn chỉ có truy cập với localhost. Để cấu hình Redis chấp nhận các kết nối từ xa, hãy làm như sau:

Mở tệp cấu hình redis: ``# nano /etc/redis/redis.conf``

Tìm đến dòng bind ``127.0.0.1`` và thêm địa chỉ IP riêng của bạn hoặc ``0.0.0.0`` cho mạng ngoài:

![](/img/Redis_Bind_0000.png)

Sau đó, chỉ định mật khẩu cần thiết cho cấu hình Redis với thuộc tính ``requirepass``.

![](/img/Redis_requirepass.png)

Để các sửa đổi có hiệu lực, ta phải khởi động lại dịch Redis:

``# systemctl restart redis-server``

Để kiểm tra xem Redis có đang nghe trên cổng ``6379`` không sau khi bạn đã thực hiện các điều chỉnh ở trên:

``# ss -an | grep 6379``

![](/img/Redis_6379.png)

Nếu như Redis chưa nghe trên cổng 6378 thì ta phải cho mở cổng 6379:

``# ufw allow 6379/tcp``

Bây giờ bạn kiểm tra các cấu hình đã chạy chưa bằng cách chạy lệnh sau để truy cập:

``# redis-cli``

Xác thực danh tính của bạn bằng cách sử dụng từ khóa “AUTH” trong tệp cấu hình, cùng với mật khẩu mà bạn đã thiết lập trong các bước trước đó

``AUTH "password"``

![](/img/Redis_AUTH.png)

Ping Redis để đảm bảo rằng nó đang hoạt động đúng cách.

![](/img/Redis_ping_v2.png)

### b. Cấu hình Unix Socket Redis

Cấu hình Redis sử dụng Unix socket thay vì kết nối TCP/IP có nhiều lợi ích, đặc biệt là trong trường hợp bạn đang sử dụng Redis trên cùng một máy chủ với ứng dụng (ví dụ như WordPress), như là:

* **Tăng hiệu suất**

  + Unix socket là một cơ chế giao tiếp giữa các tiến trình (inter-process communication – IPC) trên cùng một máy chủ, giúp loại bỏ hoàn toàn việc phải qua lớp mạng và giao thức TCP/IP.
      
  + Khi bạn sử dụng Unix socket, Redis và ứng dụng (WordPress) có thể giao tiếp trực tiếp thông qua hệ thống file của máy chủ, điều này giúp giảm độ trễ và cải thiện hiệu suất. Quá trình này ít phức tạp hơn so với việc sử dụng kết nối TCP/IP, vì không cần thực hiện các bước xử lý mạng như phân mảnh gói tin, quản lý kết nối, hay mã hóa dữ liệu.

* **Tăng cường bảo mật**

  + Kết nối qua TCP/IP có thể bị lộ thông qua mạng nội bộ hoặc bị tấn công từ bên ngoài nếu không có các biện pháp bảo mật thích hợp (ví dụ: firewall, mật khẩu mạnh).
  
  + Sử dụng Unix socket giúp giới hạn kết nối Redis trong phạm vi của máy chủ. Chỉ các ứng dụng trên cùng máy chủ mới có thể truy cập vào Redis thông qua socket. Điều này loại bỏ rủi ro tấn công từ xa và tăng cường bảo mật mà không cần xác thực qua mạng.

* **Giảm chi phí tài nguyên**

  + Sử dụng TCP/IP yêu cầu hệ thống quản lý kết nối mạng, lưu thông tin và thực hiện các giao thức phức tạp. Điều này tiêu tốn một phần tài nguyên của CPU và bộ nhớ.
  
  + Unix socket đơn giản hơn nhiều, không yêu cầu giao thức mạng và giảm tải hệ thống trong quá trình xử lý dữ liệu.

* **Đơn giản hóa cấu hình mạng**

  + Khi sử dụng Unix socket, bạn không cần phải cấu hình firewall, không phải lo lắng về việc mở cổng Redis ra ngoài và các thiết lập bảo mật phức tạp khác.
  
  + Điều này giúp cấu hình đơn giản hơn, đồng thời tăng cường khả năng quản lý trên hệ thống cục bộ.

*  **Sử dụng trong môi trường không phân tán**  
  + Nếu bạn không có nhu cầu chia sẻ Redis cho các máy chủ khác hoặc trong môi trường phân tán, thì việc sử dụng Unix socket là lựa chọn hợp lý nhất. Nó giúp giữ Redis hoạt động nội bộ trong cùng máy chủ, mà không cần mở cổng ra ngoài.

**Khi nào không nên sử dụng Unix socket?**

Nếu Redis cần được truy cập từ nhiều máy chủ khác nhau qua mạng, thì việc sử dụng Unix socket không khả thi. Trong trường hợp đó, bạn cần sử dụng TCP/IP để cho phép các máy chủ khác kết nối với Redis.

Muốn cấu hình Unix socket cho Redis ta mở file cấu hình của Redis:

``# nano /etc/redis/redis.conf``

Ta tìm dòng ``bind 127.0.0.1`` hoặc các dòng bind IP tương tự, ta cho dòng này comment hoặc vô hiệu hoá

![](/img/Redis_comment_bind.png)

Tiếp theo, ta tìm các dòng Unix Socket và bật nó lên
            
    unixsocket /var/run/redis/redis-server.sock  # Đặt đường dẫn đến Unix socket file
    unixsocketperm 770                    # Đặt quyền truy cập cho socket

![](/img/Redis_Unixsocket.png)

**Tạo và gán quyền Unix Socket**

Tạo thư mục cho socket và gán quyền cho Redis:

    # mkdir /var/run/redis
    # chown redis:redis /var/run/redis

Bạn cấp quyền 770 cho thư mục:

    # chmod 770 /var/run/redis

Đảm bảo nhóm www-data (người dùng chạy Nginx) có quyền truy cập vào socket:

    # usermod -aG redis www-data

Ta khỏi động lại Redis,0 Nginx và PHP-FPM để áp dụng cấu hình:

    # systemctl restart redis-server
    # systemctl restart nginx
    # systemctl restart php8.2-fpm


**Chỉnh sửa file wp-config.php**

Các bạn tìm tới nơi lưu trữ file ``wp-config.php`` của các bạn và sau đó ta thêm các dòng sau

    //Redis cache
    define('WP_REDIS_SCHEME', 'unix');
    define('WP_REDIS_PATH', '/var/run/redis/redis-server.sock'); 
    define('WP_REDIS_PREFIX', 'https://website1.dns.info.vn');
    define('WP_REDIS_TIMEOUT', 60 );
    define('WP_REDIS_READ_TIMEOUT', 60 );
    define('WP_REDIS_MAXTTL', '900');
    define('WP_REDIS_SELECTIVE_FLUSH', true);


> [!WARNING]  
> Lưu ý thêm nội dung nằm dưới thẻ mở ``<?php``

Trong đó:
  * ``define('WP_REDIS_PATH','/var/run/redis/redis.sock');`` :các bạn thay thành địa chỉ chứa socket của các bạn
  
  * ``define( 'WP_REDIS_PREFIX', 'https://website1.dns.info.vn');`` : thay thành địa chỉ website của các bạn

![](/img/Redis_Unixsocket_config.png)

Nếu các bạn muốn 2 website dùng chung một Unix Socket Redis bằng cách tách dữ liệu của chúng. Ta sử dụng các ``Prefix khác nhau (WP_REDIS_PREFIX)``, ``Database khác nhau (WP_REDIS_DATABASE)`` và ``Key salt riêng (WP_CACHE_KEY_SALT)`` cho từng website.

Ví dụ:

Trong file ``wp-config.php`` của ``website1.dns.info.vn`` ta cấu hình như sau:

    define('WP_REDIS_SCHEME', 'unix');
    define('WP_REDIS_PATH', '/var/run/redis/redis-server.sock'); 
    define('WP_REDIS_PREFIX', 'https://website1.dns.info.vn');
    define('WP_REDIS_TIMEOUT', 60 );
    define('WP_REDIS_READ_TIMEOUT', 60 );
    define('WP_REDIS_MAXTTL', '900');
    define('WP_REDIS_SELECTIVE_FLUSH', true);
    define('WP_CACHE_KEY_SALT', 'site1_'); 
    define('WP_REDIS_DATABASE', 0);             # Database của website1.dns.info.vn là 0

còn ``wp-config.php`` của ``website2.dns.info.vn`` thì cấu hình như sau:

    define('WP_REDIS_SCHEME', 'unix');
    define('WP_REDIS_PATH', '/var/run/redis/redis-server.sock'); 
    define('WP_REDIS_PREFIX', 'https://website2.dns.info.vn'); // Thay đổi prefix để phân biệt dữ liệu giữa 2 website
    define('WP_REDIS_TIMEOUT', 60 );
    define('WP_REDIS_READ_TIMEOUT', 60 );
    define('WP_REDIS_MAXTTL', '900');
    define('WP_REDIS_SELECTIVE_FLUSH', true);
    define('WP_CACHE_KEY_SALT', 'site2_'); // Key salt riêng cho website thứ hai
    define('WP_REDIS_DATABASE', 1);         # Database của website2.dns.info.vn là 1

Nếu bạn muốn sử dụng nhiều Unix socket (mỗi website có một Unix socket riêng), bạn cần phải chạy nhiều Redis instances  trên server, mỗi instance có file cấu hình riêng với Unix socket riêng.

* **Bước 1: Sao chép và tùy chỉnh file cấu hình Redis**

Redis sử dụng file cấu hình mặc định là ``/etc/redis/redis.conf``. Để chạy nhiều instances, bạn cần tạo bản sao của file này cho mỗi instance.

      # cp /etc/redis/redis.conf /etc/redis/redis2.conf

Mở file cấu hình Redis mới vừa sao chép và sửa lại một số thông số để mỗi instance chạy độc lập.

      # nano /etc/redis/redis2.conf

Cấu hình file instance mới của redis như sau:

      unixsocket /var/run/redis/redis-server2.sock
      unixsocketperm 770

Redis cần file PID riêng cho từng instance để quản lý quá trình:

      pidfile /var/run/redis/redis-server2.pid

Nếu bạn muốn ghi log riêng cho từng instance, hãy thay đổi đường dẫn file log:

      logfile /var/log/redis/redis-server2.log

Bạn cũng cần chỉ định đường dẫn lưu trữ dữ liệu riêng cho mỗi instance Redis để tránh xung đột:

* **Bước 2: Tạo thư mục cho dữ liệu và Unix socket**

Tạo thư mục cho Unix socket và dữ liệu Redis thứ hai:

    # mkdir /var/lib/redis2
    # chown redis:redis /var/lib/redis2
    # chmod 770 /var/run/redis

* **Bước 3: Tạo service cho Redis instance thứ hai**

Redis sử dụng systemd để quản lý dịch vụ. Bạn sẽ cần tạo file service mới cho instance Redis thứ hai bằng cách sao chép file service mặc định của Redis:

    # cp /lib/systemd/system/redis-server.service /lib/systemd/system/redis-server2.service

Mở file ``redis-server2.service`` và thay đổi tham số chỉ định đến file cấu hình của instance thứ hai:

    # nano /lib/systemd/system/redis-server2.service

Tìm dòng ``ExecStart`` và thay đổi nó để trỏ đến file cấu hình Redis thứ hai:

    ExecStart=/usr/bin/redis-server /etc/redis/redis2.conf --supervised systemd --daemonize no

Sau khi chỉnh sửa xong file service, bạn cần tải lại cấu hình systemd:

    # systemctl daemon-reload

* **Bước 4: Khởi động và kích hoạt Redis instance thứ hai**

Khởi động instance Redis thứ hai:

    # systemctl start redis-server2

Kiểm tra trạng thái: Kiểm tra xem instance Redis thứ hai đã khởi động thành công chưa:

    # systemctl status redis-server2

* **Bước 5: Cấu hình wp-config.php cho website2.dns.info.vn**

  Ta đổi lại ``WP_REDIS_PATH`` của ``website2.dns.info.vn`` cho khớp với instance mới của Redis

      define('WP_REDIS_PATH', '/var/run/redis/redis-server2.sock');

![](/img/Redis_Unixsocket_website2.png)

# END
