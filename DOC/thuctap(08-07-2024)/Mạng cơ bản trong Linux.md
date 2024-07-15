# MẠNG CƠ BẢN TRONG LINUX

# MỤC LỤC

- [MẠNG CƠ BẢN TRONG LINUX](#mạng-cơ-bản-trong-linux)
- [MỤC LỤC](#mục-lục)
  - [I. Cấu hình mạng](#i-cấu-hình-mạng)
    - [Cấu hình IP tĩnh và động](#cấu-hình-ip-tĩnh-và-động)
  - [II. Kiểm tra kết nối mạng](#ii-kiểm-tra-kết-nối-mạng)
- [END](#end)


>[!WARNING]
>Mọi câu lệnh đều được chạy dưới quyền ``root``, nếu không chạy quyền ``root`` thì thêm ``sudo`` vào trước các câu lệnh. 

## I. Cấu hình mạng

### Cấu hình IP tĩnh và động


* **Xác định địa chỉ IP hiện tại**

    Hầu hết các máy chủ hay máy chủ ảo VPS cloud server gì đó ngày nay đều có một card Ethernet để nối vào mạng internet WAN. Khi cài đặt Linux, thiết bị này thường được gọi là eth0 tuỳ vào máy bạn sẽ có cái tên khác nhau.
    
    Sử dụng câu lệnh `# ifconfig -a` hoặc ``# ip a`` để xác định địa chỉ IP của card này, cũng như của các card mạng khác.

    ![](/img/ip_a.png)


* **Cấu hình netplan**

    Các file netplan thường nằm trong đường dẫn ``/etc/netplan`` và các file đó thường có phần mở rộng là ``.yaml``

    ![](/img/netplan.png)

    Như ở đây file .yaml trên máy mình có tên là ``50-cloud-init.yaml``

    Các bạn sử dụng trình soạn thảo ``vi``, ``vim`` hay ``nano`` để sạn thảo cho file này.

    Tại đây thì mình dùng ``nano``: ``# nano /etc/netplan/50-cloud-init.yaml``

    ![](/img/menunano.png)

    Một điều bạn cần nắm trong file cấu hình này là mỗi tếp Netplan sẽ bắt đầu bằng từ khóa network và có ít nhất 2 phần tử bắt buộc đó là.

    ``network:`` Đây là khóa gốc cho cấu hình mạng.

    `version:` Chỉ định phiên bản của Netplan.

    Các bạn soạn thảo file ``.yaml`` như sau:

    ![](/img/nanoyaml.png)


    Trong đó: 

    ``renderer:`` Chỉ định công cụ quản lý mạng (**networkd** hoặc **NetworkManager**)

    ``ethernets:`` Dùng để cấu hình các giao diện mạng Ethernet.

    ``dhcp4: no``: Tắt DHCP vì bạn đang sử dụng IP tĩnh.

    ``addresses:`` Thiết lập địa chỉ IP tĩnh.

    ``routes:`` Sử dụng phần này để định nghĩa route và gateway thay vì gateway4.
        
    * ``to:`` Địa chỉ mạng đích.   
    * ``via:`` Địa chỉ IP của gateway.
    * ``metric:`` Độ ưu tiên của route (không bắt buộc).

    ``nameservers:`` Cấu hình DNS servers.

    Đó là cấu hình IP tĩnh, muốn cấu hình IP động ta đổi ``dhcp4: no`` và ``dhcp4: true`` vào file .yaml

    ![](/img/nanoyaml_dynamic.png)


* **Lưu file và xác minh**

    Dùng lệnh ``netplan apply`` để áp cấu hình mạng mới và dùng lệnh ``ip -a`` để kiểm tra

    ![](/img/savenetplan.png)

    
## II. Kiểm tra kết nối mạng

Có 3 lệnh để kiểm tra kết nối mạng ``ping``, ``traceroute``, và ``netstat`` tuy vậy về mục đích sử dụng thì chúng nó lại khác nhau.

**PING**
* **Mục đích:** ping được sử dụng để kiểm tra kết nối mạng và đo thời gian đáp ứng từ một thiết bị mạng khác.

* **Hoạt động:** Gửi gói tin ICMP (Internet Control Message Protocol) tới đích và đợi phản hồi. Nếu máy chủ hoặc thiết bị đích phản hồi, ping sẽ hiển thị thời gian mà gói tin mất đi và thời gian mà gói tin trả về (round-trip time).

* **Sử dụng thường gặp:** Kiểm tra xem một thiết bị có kết nối mạng hoạt động hay không, kiểm tra độ trễ mạng, và kiểm tra sự ổn định của kết nối.

**Ping thử tới mạng bên ngoài bởi cấu hình netplan ta vừa áp**

![](/img/pinggoogle.png)

**Traceroute**

* **Mục đích:** traceroute được sử dụng để theo dõi và hiển thị đường đi mà gói tin mạng đi qua từ máy tính của bạn đến một đích nhất định.

* **Hoạt động:** traceroute gửi các gói tin mạng với TTL (Time-To-Live) tăng dần đến đích. Mỗi bước đi của gói tin sẽ được lưu lại và hiển thị cho người dùng, cho biết các nút mạng (router) mà gói tin đã đi qua và thời gian mà gói tin đến từng nút đó.

* **Sử dụng thường gặp:** Xác định đường đi và giúp phát hiện vấn đề nếu có lỗi trong mạng (ví dụ như gói tin bị mất hoặc chậm).

**Thực hành sử dụng traceroute**
  * **Tải tracerouter về**
  
    ![](/img/apttraceroute.png)

  * **Cú pháp câu lệnh traceroute:** ``# traceroute [options] [host_address]``

    | Tùy chọn    | Mô tả                                                     |
    |-------------|------------------------------------------------------------|
    | `-I`        | Sử dụng gói tin giao thức ICMP ECHO                        |
    | `-U`        | Sử dụng gói tin giao thức TCP SYN                          |
    | `-w <number>` | Cấu hình thời gian chờ phản hồi, tính bằng giây          |
    | `-f <number>` | Chỉ định giá trị TTL bắt đầu, mặc định là 1                |
    | `-q <number>` | Cấu hình số gói tin phản hồi ở mỗi hop, mặc định là 3     |
    | `-m <number>` | Cấu hình số hops tối đa (giá trị TTL tối đa), mặc định là 30 |


    ![](/img/traceroute.png)


**Netstat**

* **Mục đích:** netstat là công cụ để xem và phân tích thông tin về các kết nối mạng, bảng định tuyến, giao diện mạng và các thống kê liên quan đến mạng.

* **Hoạt động:** netstat hiển thị danh sách các kết nối mạng đang mở, bao gồm cả kết nối TCP và UDP, và các cổng mạng đang được sử dụng bởi các ứng dụng hoặc dịch vụ khác nhau trên máy tính.

* **Sử dụng thường gặp:** Để kiểm tra các kết nối mạng hiện đang mở, tìm kiếm thông tin về các cổng mạng và các ứng dụng đang sử dụng chúng, kiểm tra tình trạng mạng và các vấn đề liên quan đến kết nối mạng.

**Thực hành sử dụng Netstat**

* **Cú pháp câu lệnh netstat:** ``# netstat [options]``

    | Tùy chọn | Mô tả                                                                |
    |----------|-----------------------------------------------------------------------|
    | `-a`     | Hiển thị tất cả các sockets, bao gồm listening và non-listening      |
    | `-l`     | Hiển thị các socket đang lắng nghe                                     |
    | `-t`     | Chỉ hiển thị các kết nối TCP                                           |
    | `-u`     | Chỉ hiển thị các kết nối UDP                                           |
    | `-n`     | Hiển thị địa chỉ IP thay vì dịch vụ và tên                             |
    | `-p`     | Hiển thị PID của từng socket                                           |
    | `-r`     | Hiển thị bảng định tuyến                                               |
    | `-s`     | Pull và hiển thị thống kê mạng được sắp xếp theo giao thức            |
    | `-i`     | Hiển thị danh sách các giao diện mạng                                  |

    ![](/img/netstat.png)

# END