# Cấu hình BIND trên CentOS

## Mục lục
- [Cấu hình BIND trên CentOS](#cấu-hình-bind-trên-centos)
  - [Mục lục](#mục-lục)
  - [Giới thiệu sơ lược về BIND](#giới-thiệu-sơ-lược-về-bind)
  - [Cài đặt BIND](#cài-đặt-bind)
  - [Bắt đầu dịch vụ BIND](#bắt-đầu-dịch-vụ-bind)
  - [Cấu hình BIND trên Server](#cấu-hình-bind-trên-server)
  - [Tạo các vùng BIND](#tạo-các-vùng-bind)
  - [Cấu hình tập tin vùng BIND](#cấu-hình-tập-tin-vùng-bind)
  - [Cấu hình trên máy Client](#cấu-hình-trên-máy-client)
  - [Sử dụng lệnh dig hoặc nslookup để truy vấn tên miền](#sử-dụng-lệnh-dig-hoặc-nslookup-để-truy-vấn-tên-miền)
- [END](#end)

## Giới thiệu sơ lược về BIND

BIND (Berkeley Internet Name Domain) là một phần mềm hệ thống máy chủ tên miền cơ bản và phổ biến nhất hiện nay. BIND được sử dụng trên hầu hết các máy chủ phân giải tên miền trên toàn thế giới.

## Cài đặt BIND

Trong bài lab này mình có 2 máy ảo CentOS, một máy server và một máy client chúng có ip lần lượt là:

* **Server**: ``192.168.3.152/24``
* **Client**: ``192.168.3.198/24``

Trên cả 2 máy ảo ta đều cài đặt BIND, để cài đặt BIND ta sử dụng câu lệnh sau:

``# yum install bind -y``

![](/img/bind_install.png)


## Bắt đầu dịch vụ BIND

Khi các gói BIND của bạn được cài đặt, bạn cần khởi động dịch vụ của nó và cho phép nó tự khởi động sau mỗi lần khởi động lại, để bạn không phải bắt đầu thủ công mỗi lần. Chúng ta hãy chạy các lệnh sau để làm như vậy và sau đó kiểm tra trạng thái của dịch vụ BIND.

``# systemctl enable named``

``# systemctl start named``

``# systemctl status named``

![](/img/bind_status.png)

## Cấu hình BIND trên Server

Cấu hình của BIND bao gồm nhiều tệp như tệp cấu hình chính và named.conf. Tên các tệp này bắt đầu bằng named vì đó là tên của tiến trình mà BIND chạy (với named được rút gọn từ “name daemon”, như trong “domain name daemon”). Bạn sẽ bắt đầu bằng cách cấu hình tệp named.conf

``# nano /etc/named.conf`` để chỉnh sửa file named.conf

![](/img/bind_blockoption.png)


## Tạo các vùng BIND

Bây giờ ta sẽ thêm các vùng chuyển tiếp và đảo ngược trong tệp ‘name.conf’ cho miền của chúng ta. Vì vậy, để thiết lập chỉnh sửa vùng chuyển tiếp /etc/named.conf theo cách như vậy để đặt các cấu hình sau.

``# nano /etc/named.conf``

**Cấu hình Forward Zone**

![](/img/bind_forwardzone.png)

**Trong đó:**

* **thuctap.azdigi.info**: là tên của domain.

* **type master**: Xác định rằng máy chủ DNS này là máy chủ chính cho vùng DNS

* **file "thuctap.azdigi.info.db"**: Đường dẫn tới tệp chứa các bản ghi DNS cho vùng "thuctap.azdigi.info".

* **allow-update { none; }**: để chỉ định rằng không ai được phép cập nhật các bản ghi DNS cho zone.

**Cấu hình Reverse Zone tương tự**

![](/img/bind_reversezone.png)

## Cấu hình tập tin vùng BIND

* **Cấu hình file Forward Zone**

Forward zone file là nơi bạn xác định các bản ghi DNS để tra cứu DNS chuyển tiếp. Tức là, khi DNS nhận được một truy vấn tên nó sẽ tìm kiếm trong forward zone file để phản hồi địa chỉ IP riêng tương ứng.

``# nano /var/named.azdigi.info.db``

![](/img/bind_forwardzonefile.png)

* **Cấu hình file Reverse Zone**

Reverse zone files là nơi bạn xác định các bản ghi DNS PTR để tra cứu các DNS ngược. Đó là, khi DNS nhận được một truy vấn bằng địa chỉ IP nó sẽ tìm kiếm trong các reverse zone files để phản hồi FQDN tương ứng

``# nano /var/named/192.168.3.db``

![](/img/bind_reversezonefile.png)

* **Kiểm tra cấu hình**

Ta sử dụng lần lượt các câu lệnh để kiểm tra xem ta có làm sai bước nào không.

``# named-checkconf``

``# named-checkzone thuctap.azdigi.info /var/named.azdigi.info.db``

``# named-checkzone 3.168.192.in-addr.arpa /var/named/192.168.3.db``

![](/img/bind_check.png)

chúng ta khởi động lại BIND để chạy cấu hình.

## Cấu hình trên máy Client

Trên máy client ta sẽ cấu hình DNS để tra cứu tên miền

``# nano /etc/resolv.conf``

Ta thêm dòng nameserver 192.168.3.152

![](/img/bind_resolv.png)

sau đó ta khởi động lại mạng ``systemctl restart NetworkManager``

## Sử dụng lệnh dig hoặc nslookup để truy vấn tên miền

Phòng trường hợp tường lửa đang hoạt động, ta cần phải cho phép DNS vượt tường lửa nếu không chúng ta không thể dùng máy client truy vấn được máy chủ.

``# firewall-cmd --add-service=dns --permanent``

``# firewall-cmd --reload``

Ta sử dụng lệnh ``dig`` để truy vấn

``# dig thuctap.azdigi.info``

![](/img/bind_dig.png)

Ta sử dụng lệnh ``nslookup`` để truy vấn

``# nslookup thuctap.azdigi.info``

![](/img/bind_nslookup.png)


# END