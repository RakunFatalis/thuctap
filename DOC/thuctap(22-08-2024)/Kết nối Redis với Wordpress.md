# Kết nối Redis với Wordpress

# Mục lục

- [LEMP Stack trên Ubuntu 20.04 và WordPress](#i-giới-thiệu-redis-cache)



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

![](/thuctap/img/WordPress_login.png)

* **Bước 2: Cài đặt Redis Object Cache**

Bạn truy cập vào phần **Plugins(1)** -> **Add New Plugin(2)** -> **Nhấp vào ô Search và gõ "Redis Object Cache(3)"** -> **Và nhấp vào ô Install Now của Redis Object Cache(4)**

![](/thuctap/img/WordPress_Plugin_Redis.png)

Sau khi tải xong các bạn nhấn vào ô Activate để kích hoạt plugin

![](/thuctap/img/WordPress_Activated_Redis.png)

* **Bước 3: Khởi động Redis Object Cache**

Sau khi đã kích hoạt plugin Redis Object Cache thì các bạn vào phần Settings -> Redis để vào trang plugin của Redis.

![](/thuctap/img/WordPress_Setting_Redis.png)

* **Bước 4. Khởi động Redis**

Sau khi các bạn đã vào trang plugin của Redis các bạn nhấp vào ô ``Enable Object Cache`` để kích hoạt Redis lên

![](/thuctap/img/WordPress_Redis_Enable.png)

Đây là sau khi kích hoạt thành công

![](/thuctap/img/WordPress_Redis_Succ.png)

### b. Trên Linux

Thông thường thì các gói Redis sẽ có sẵn trong kho mặc định của hệ điều hành Linux. Để cài đặt Redis các bạn hãy nhập lệnh sau:

      # apt update -y
      # apt install redis-server -y

Sau đó, hãy cho phép Redis khởi động lại cùng với hệ thống khi hệ thống khởi động.

      # systemctl enable redis-server

Kiểm tra xem Redis đã khởi động chưa:

      # systemctl status redis

