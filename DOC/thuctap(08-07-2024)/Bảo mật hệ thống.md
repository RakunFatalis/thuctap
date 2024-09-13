# BẢO MẬT HỆ THỐNG

# MỤC LỤC
- [BẢO MẬT HỆ THỐNG](#bảo-mật-hệ-thống)
- [MỤC LỤC](#mục-lục)
  - [I. Firewall](#i-firewall)
    - [1. Cài đặt](#1-cài-đặt)
    - [2. Cấu hình](#2-cấu-hình)
  - [II. SSH](#ii-ssh)
    - [SSH Key là gì?](#ssh-key-là-gì)
    - [1. Cài đặt](#1-cài-đặt-1)
    - [Cấu hình bảo mật SSH.](#cấu-hình-bảo-mật-ssh)
- [END](#end)



>[!WARNING]
>Mọi câu lệnh đều được chạy trên bản distro Linux: Ubuntu 2
>Mọi câu lệnh đều được chạy dưới quyền ``root``, nếu không chạy quyền ``root`` thì thêm ``sudo`` vào trước các câu lệnh. 

## I. Firewall

Firewall là một phần quan trọng trong bảo mật hệ thống, giúp ngăn chặn các kết nối không mong muốn và bảo vệ các dịch vụ trên máy chủ Linux. Các công cụ phổ biến để cấu hình firewall trên Linux bao gồm ``ufw``, ``firewalld``, và ``iptables``. Dưới đây là hướng dẫn chi tiết để cài đặt và cấu hình từng công cụ này.

### 1. Cài đặt

**Cài đặt iptables**

* Kiểm tra xem iptables đã được cài đặt chưa

    ``# iptables -V``

    ![](/img/iptables_v.png)

* Nếu chưa có, cài đặt iptables

    ``# apt install iptables``

    ![](/img/iptables_i.png)

**Cài đặt firewalld**

* Kiểm tra xem firewalld đã được cài đặt chưa:

    ``# systemctl status firewalld``

    ![](/img/firewalld_v.png)

* Nếu chưa có, cài đặt firewalld

    ``# apt install firewalld``

    ![](/img/firewalld_i.png)

    ``# yum install firewalld`` Lệnh này dùng cho CentOS/RHEL

    ``# dnf install firewalld`` Lệnh này dùng cho Fedora

* Bật firewalld

    ``# systemctl start firewalld``
    
    ``# systemctl eanble firewalld``

**Cài đặt ufw**

* Kiểm tra xem ufw đã được cài đặt chưa

    ``# ufw status``

    ![](//img/ufw_v.png)

* Nếu chưa có, cài đặt ufw:

    ``# apt install ufw``

    ![](/img/ufw_i.png)

### 2. Cấu hình

**Cấu hình  bằng ufw**

* Kịch hoạt ufw sau khi cài đặt 

    ``# ufw enable``

* Kiểm tra đã kích hoạt ufw chưa

    ``# ufw status``

* Khôi phục firewall UFW về cấu hình mặc định

    ``# ufw reset``

![](/img/ufw_check.png)


* Thiết lập chính sách mặc định


    ``# ufw default deny incoming``

    ``# ufw default allow outgoing``

    ![](/img/ufw_default.png)

* Cho phép các port cần truy cập vào server

    Mặc định firewall ufw sẽ chặn toàn bộ kết nối đến server.

    Để thực hiện mở một port (cổng) bất kỳ bạn có thể thực hiện cú pháp lệnh như sau:

    ``# ufw allow [port]/[protocol]``

    Ví dụ : mở các port 80, 443, 3306 và 8080

    ![](/img/ufw_allow_port.png)


* Chặn truy cập đến một port.

    Các port không được allow sẽ tự động chặn kết nối từ bên ngoài.

    Ngoài ra, để chặn một port cụ thể có thể sử dụng cú pháp với tùy chọn ``deny ``như sau:

    ``# ufw deny [port]/[protocol]``

    Ví dụ : mình sẽ đóng port 80, 443

    ![](/img/ufw_deny_port.png)

* Ngoài ra ufw cho phép thực hiện lệnh allow và deny với loại service cụ thể. Ví dụ: sử dụng mysql thay vì mởi port 3306, sử dụng http hay https thay vì các port 80, 443, cụ thể:

    ``# ufw deny mysql``

    ``# ufw allow http``

    ``# ufw allow https``

    ![](/img/ufw_detail_servic.png)

* Cho phép môt IP hoặc một range IP truy cập đến server.
    
    ``# ufw deny from $Your_IP``

    Ví dụ:  chặn truy cập từ IP 172.20.1.126 như sau.

    ![](/img/ufw_allow_ip.png)

* Cho phép IP kèm port nhất định vào server

    Lệnh cho phép một IP hoặc một range IP truy cập đến một Port cụ thể trên server:

    ``# ufw allow from [ip/range-ip] to any port [port-number]``

    Ví dụ: câu lệnh cho phép IP 192.168.72.1 truy cập đến port 22 và 3306

    ![](/img/ufw_allow_ip_to_port.png)

* Xóa bỏ rule firewall cấu hình trước đó.

    Kiểm tra các rule hiện có với số định danh. Lệnh:

    ``# ufw status numbered``

    ![](/img/ufw_idnumber.png)

* Xác định chính xác rule muốn xóa với số định danh tương ứng

    Thực hiện lệnh xóa rule với lệnh:

    ``# ufw delele [number]``

    Ví dụ: thực hiện xóa rule cho phép truy cập đến port SSH (22)

    ![](/img/ufw_delete_rule.png)

* Bật hoặc tắt ipv6 trên firewal UFW

    Trong trường hợp server sử dụng IPv6, cần đảm bảo rằng IPv6 được bật trong UFW. 

    Mở file cấu hình UFW ở /etc/default/ufw và tiến hành điều chỉnh.
    Nếu dòng ``IPV6=no`` bạn hãy chuyển sang ``YES`` để kích hoạt và ngược lại nếu muốn tắt thì chọn ``no``.

    ![](/img/ufw_IPV6.png)

    Sau cùng sử dụng lệnh sau để reload lại cấu hình

    ``# ufw reload``

    ![](/img/ufw_reload.png)

## II. SSH

### SSH Key là gì?

SSH Key là một cặp khóa mật mã được sử dụng để xác thực người dùng khi kết nối với máy chủ SSH. Khóa công khai được lưu trữ trên máy chủ SSH, trong khi khóa bí mật được lưu trữ trên máy khách SSH. Khi người dùng kết nối với máy chủ SSH, máy chủ sẽ sử dụng khóa công khai để tạo một dấu vân tay. Máy khách SSH sau đó sẽ sử dụng khóa bí mật để tạo một dấu vân tay tương ứng. Nếu hai dấu vân tay này khớp nhau, thì người dùng sẽ được xác thực thành công.
### 1. Cài đặt


* Sử dụng câu lệnh để tải OpenSSH Server:

    ``# apt install openssh-server``

    ![](/img/install_openssh.png)


* Kiểm tra OpenSSH Server đã kích hoạt chưa;

    ``# systemctl status ssh``

    ![](/img/checkssh.png)

* Kích hoạt SSH lên

    ``# systemctl enable ssh``

    ![](/img/sshenable.png)

    Khởi động lại SSH để chạy:

    ``# systemctl restart ssh``

* **Tạo SSH key**

    ``# ssh-keygen -t rsa``

    ![](/img/ssh_keygen.png)


### Cấu hình bảo mật SSH.

Vào đường dẫn ``/etc/ssh`` để kiếm file có tên ``sshd_config``

![](/img/ssh_location.png)

Sử dụng trình thảo ``vi`` hoặc ``nano`` để cấu hình file

![](/img/ssh_config.png)


File sshd_config là file cấu hình chính cho SSH Daemon (sshd). Mỗi dòng trong file này đại diện cho một thiết lập cụ thể của dịch vụ SSH.

Dưới đây là một số dòng thông dụng để bảo mật SSH
* **Port 22**
    
    Chỉ định cổng mà dịch vụ SSH sẽ lắng nghe. Mặc định là cổng 22, bạn có thể thay đổi để tăng cường bảo mật.

* **PermitRootLogin yes/no/prohibit-password/without-password/forced-commands-only**

    Xác định liệu người dùng root có được phép đăng nhập qua SSH hay không. Các tuỳ chọn khác nhau cho phép hoặc cấm root đăng nhập theo nhiều cách khác nhau.

* **PasswordAuthentication yes/no**

    Bật hoặc tắt xác thực bằng mật khẩu. Tắt tùy chọn này sẽ yêu cầu sử dụng phương thức xác thực khác (ví dụ: khóa công khai).

# END