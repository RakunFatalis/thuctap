# Nginx

# Mục lục
- [Nginx](#nginx)
- [Mục lục](#mục-lục)
- [I. Cài đặt Nginx](#i-cài-đặt-nginx)
  - [1. Hướng dẫn cài đặt Nginx bằng lệnh Yum](#1-hướng-dẫn-cài-đặt-nginx-bằng-lệnh-yum)
  - [2. Hướng dẫn cài đặt Nginx bằng complier từ mã nguồn](#2-hướng-dẫn-cài-đặt-nginx-bằng-complier-từ-mã-nguồn)
- [II. File cấu hình và file log của Nginx](#ii-file-cấu-hình-và-file-log-của-nginx)
  - [1. File cấu hình](#1-file-cấu-hình)
  - [2. File Log của Nginx](#2-file-log-của-nginx)
- [III. File cấu hình chính của Nginx](#iii-file-cấu-hình-chính-của-nginx)
- [END](#end)



# I. Cài đặt Nginx

## 1. Hướng dẫn cài đặt Nginx bằng lệnh Yum 

**Bước 1: Cập Nhật Hệ Thống**

Trước khi ta cài đặt Nginx, ta cần phải cập nhật các gói trong hệ thống Linux lên phiên bản mới nhất

``# yum update``

**Bước 2: Cài Đặt Nginx**

Sử dụng yum để cài đặt Nginx từ kho lưu trữ mặc định của CentOS.

``# yum install nginx ``

![](/img/install_nginx.png)

**Bước 3: Khởi Động Dịch Vụ Nginx**

Sau khi cài đặt xong, khởi động dịch vụ Nginx và kiểm tra dịch vụ đã chạy chưa

``# systemctl start nginx``

``# systemctl status nginx``

![](/img/nginx_status.png)

**Bước 4: Cho phép các port HTTP và HTTPS:**

Bạn cần phải cấu hình tường lửa để Nginx có thể đáp ứng dịch vụ qua internet. Thông thường CentOS sẽ mặc định chặn truy cập vào port 80 và 443, điều này sẽ trực tiếp chặn các traffic của Nginx. Để cho phép các traffic HTTP và HTTPS ta thực thi lần lượt các lệnh sau:

``# firewall-cmd --permanent --zone=public --add-service=http`` 

``# firewall-cmd --permanent --zone=public --add-service=https``

``# firewall-cmd --reload``

**Bước 5: Nhập IP Server để kiểm tra:**

Sau khi các bạn cài đặt thành công xong thì các bạn nhập IP Server để kiểm tra xem ta đã cài đặt thành công chưa

![](/img/Nginx_success.png)

## 2. Hướng dẫn cài đặt Nginx bằng complier từ mã nguồn

**Bước 1. Cài đặt các gói mở rộng** 

Trước tiên, bạn cần cài đặt các gói phụ thuộc cần thiết để compile Nginx.

``# yum groupinstall "Development Tools"``

``# yum install -y epel-release net-tools bind-utils net-tools automake pigz git perl perl-ExtUtils-Embed libxslt libxslt-devel libxml2 libxml2-devel gd gd-devel GeoIP GeoIP-devel gcc-c++ pcre-devel openssl-devel zlib-devel ``

**Bước 2: Tải Mã Nguồn Nginx**

Tải phiên bản mới nhất của mã nguồn Nginx từ trang web chính thức.

``# wget https://nginx.org/download/nginx-1.24.0.tar.gz``

``# tar -zxvf nginx-1.24.0.tar.gz``

``cd nginx-1.24.0``

**Bước 3: Cấu Hình, Compile Và Cài Đặt Nginx**

* **Cấu Hình Nginx (./configure)**

    Trước khi biên dịch, bạn cần cấu hình Nginx để xác định các tùy chọn và module sẽ được sử dụng. Các tùy chọn này bao gồm vị trí cài đặt, các module cần thiết, và các thư viện phụ thuộc. Lệnh ``./configure`` tạo ra các tệp Makefile cần thiết cho quá trình biên dịch dựa trên các tùy chọn mà bạn cung cấp.

    Bạn có thể kiểm tra danh sách đầy đủ các tùy chọn bằng cách chạy: ``./configure --help``

    sau đây là các module mà mình cài:

    ``./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module``

    **--prefix=/usr/local/nginx**: Chỉ định thư mục cài đặt Nginx.

    **--with-http_ssl_module**: Bật module HTTP SSL để hỗ trợ HTTPS.

    **--with-http_v2_module**: Bật module HTTP/2 để hỗ trợ HTTP/2.
    
    Các bạn lưu ý khi mình nhập thì phải cố gắng ghi hết trên 1 dòng nhá

    ![](/img/nginx_modules.png)


* **Compile Nginx (make)**

    Sau khi cấu hình xong, bạn tiến hành compile mã nguồn bằng lệnh make. Lệnh này sẽ biên dịch mã nguồn thành các tệp thực thi:

    ``# make``

* **Cài Đặt Nginx (make install)**

    Sau khi quá trình compile hoàn tất, bạn tiến hành cài đặt Nginx vào hệ thống bằng lệnh make install. Lệnh này sẽ sao chép các tệp đã biên dịch vào các thư mục đích đã được chỉ định trong bước cấu hình.

    ``# make install``

**Bước 4: Khởi Động Nginx**

Khởi động Nginx từ đường dẫn cài đặt.

``# /usr/local/nginx/sbin/nginx``

**Bước 5: Kiểm Tra Phiên Bản Nginx**

Kiểm tra phiên bản Nginx đã cài đặt.

``# /usr/local/nginx/sbin/nginx -v``

![](/img/nginx_checkver.png)


Chúng ta thực hiện việc mở port cho Nginx như bài hướng dẫn cài Nginx bằng lệnh yum


# II. File cấu hình và file log của Nginx

## 1. File cấu hình

Cấu trúc file cấu hình Nginx có dạng như sau

![](/img/nginx_structure.png)

Tất cả các file này thông thường đều nằm trong đường dẫn  **/etc/nginx**

* **nginx.conf**: Đây là tệp cấu hình chính cho máy chủ Nginx. Mọi thay đổi trong đây sẽ áp dụng cho toàn bộ mọi thứ liên quan đến Nginx.

* **modules-available** và **modules-enabled**: ta sẽ hiểu 2 thư mục này như các thư mục chứa các thư viện hỗ trợ cho nginx vậy. Nó định nghĩa các biến trong Nginx dùng để làm gì. Thông thường modules-available không có gì còn modules-enabled sẽ được link đến các thư viện ở "/usr/share/nginx/modules-available".

* **sites-available** và **sites-enabled**: hai thư mục này sẽ là 2 thư mục chứa các 2 file cấu hình mà ta thêm vào. Đầu ta sẽ thêm file cấu hình mà ta tự cấu hình vào ví dụ như virtual host sites-available sau đó mới tạo ra Symbolic Link đưa vào sites-enabled. Việc làm như vậy để khi ta muốn ngắt tạm thời cấu hình đó ra thì chỉ việc xóa Symbolic Link chứ không cần phải xóa file rồi viết lại từ đầu.

## 2. File Log của Nginx

Khi cài đặt mặc định của Nginx, Nginx sẽ ghi lại các yêu cầu vào file riêng biệt là: **access.log** và **error.log**.

File error.log của Nginx thông thường sẽ được lưu trữ tại đường dẫn **/var/log/nginx/error.log** nó lưu trữ thông tin về các lỗi bất thường của server hoặc lỗi khi xử lý yêu cầu.

Còn access.log thì nằm ở đường dẫn **/var/log/nginx/access.log**. Đây là nơi chứa những thông tin về tất cả các yêu cầu đến Nginx đã được lưu trữ. Trong log này, bạn có thể thấy người dùng đang truy cập vào các file nào, trình duyệt web họ đang sử dụng, địa chỉ IP của họ và mã trạng thái HTTP mà Nginx đã phản hồi cho mỗi yêu cầu.

![](/img/nginx_access_log.png)


Bạn có thể nắm được vài thông số qua phần phản hồi này:

``HTTP/1.1 200 OK`` cho biết Nginx đã phản hồi với mã trạng thái 200 OK thì không có lỗi xảy ra.

``Content-Length: 0``có nghĩa là tài liệu trả về có độ dài bằng không.

Yêu cầu đã được xử lý vào ``01/Aug/2024:13:59:56 +0700``.

# III. File cấu hình chính của Nginx

File cấu hình chính của Nginx là nginx.conf, nó thường nằm ở đường dẫn ``/etc/nginx/nginx.conf``

![](/img/nginx_conf_default.png)

File ``nginx.conf`` thường có dạng như sau:

![](/img/nginx_conf_structure.png)

**Các thành phần của file Nginx.conf**

1. **Global Settings (Thiết lập chung)**

    Phần Global Settings dùng để thiết lập các cấu hình chung cho toàn bộ máy chủ Nginx. Các thiết lập này ảnh hưởng đến cách Nginx chạy và quản lý các tài nguyên hệ thống

    ![](/img/Nginx_conf_global.png)

2. **Events Block**

    Events Block trong file cấu hình ``nginx.conf`` dùng để thiết lập cách Nginx xử lý các sự kiện liên quan đến kết nối mạng. Đây là nơi cấu hình các thông số ảnh hưởng đến hiệu suất và khả năng xử lý của Nginx khi có nhiều kết nối đồng thời.

    ![](/img/Nginx_conf_event.png)


3. **HTTP Block**

    HTTP Block trong file cấu hình ``nginx.conf`` là nơi chứa các thiết lập liên quan đến việc xử lý các yêu cầu HTTP. Đây là phần quan trọng nhất của cấu hình Nginx khi bạn sử dụng nó làm máy chủ web hoặc proxy ngược. Khối HTTP có thể chứa nhiều khối con như server, location, upstream, và bao gồm nhiều thiết lập khác nhau để điều chỉnh hành vi của Nginx.

    ![](/img/nginx_conf_httpblock.png)

4. **Server Block**

    Server Block trong file cấu hình ``nginx.conf`` được sử dụng để thiết lập các cấu hình liên quan đến một máy chủ ảo cụ thể. Một máy chủ ảo là một phần của máy chủ Nginx có thể xử lý các yêu cầu cho một hoặc nhiều tên miền (domain) và địa chỉ IP. Mỗi server block có thể chứa nhiều location block để xác định cách xử lý các yêu cầu đến các đường dẫn khác nhau trong máy chủ đó.

    **Lưu ý các server block thường nằm trong http block**

    ![](/img/nginx_conf_server.png)

5. **Location Block**
    
    Location Block trong file cấu hình ``nginx.conf`` được sử dụng để xác định cách Nginx xử lý các yêu cầu cho các đường dẫn cụ thể trên một máy chủ ảo (server block). Nó cho phép bạn chỉ định các hành vi khác nhau tùy thuộc vào đường dẫn của yêu cầu. Bạn có thể sử dụng ``location block`` để phục vụ tệp tĩnh, chuyển tiếp yêu cầu đến một máy chủ ngược dòng (upstream server), thực hiện chuyển hướng, hoặc thực hiện các thao tác khác.

    ![](/img/nginx_conf_location.png)

6. **SSL Configuration**

    Cấu hình SSL trong Nginx giúp bảo mật các kết nối giữa máy khách và máy chủ bằng cách mã hóa dữ liệu truyền tải
    ![](/img/Nginx_conf_SSL.png)

7. **Upstream Block**

    Khối upstream trong Nginx được sử dụng để xác định các nhóm máy chủ backend mà Nginx sẽ chuyển tiếp các yêu cầu đến. Đây là một phần quan trọng của cấu hình load balancing, giúp phân phối tải đến nhiều máy chủ backend để cải thiện hiệu suất và độ tin cậy của ứng dụng web.

    ![](/img/nginx_conf_upstream.png)

File ``nginx.conf`` có thể chứa nhiều phần cấu hình khác nhau, mỗi phần đóng vai trò thiết lập các hành vi cụ thể của Nginx. Tùy thuộc vào nhu cầu và môi trường triển khai, bạn có thể thêm hoặc điều chỉnh các phần cấu hình này để phù hợp với yêu cầu cụ thể của hệ thống.

# END