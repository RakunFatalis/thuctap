# QUẢN LÍ DỊCH VỤ VÀ TIẾN TRÌNH

# MỤC LỤC

- [QUẢN LÍ DỊCH VỤ VÀ TIẾN TRÌNH](#quản-lí-dịch-vụ-và-tiến-trình)
- [MỤC LỤC](#mục-lục)
  - [I. Quản lí dịch vụ](#i-quản-lí-dịch-vụ)
    - [1. Bắt đầu, dừng, và khởi động lại dịch vụ](#1-bắt-đầu-dừng-và-khởi-động-lại-dịch-vụ)
    - [2. Systemd là gì?](#2-systemd-là-gì)
    - [3. Thực hành](#3-thực-hành)
  - [II. Quản lí tiến trình](#ii-quản-lí-tiến-trình)
    - [1. Tiến trình là gì?](#1-tiến-trình-là-gì)
    - [2. Các lệnh để quản lí tiến trình](#2-các-lệnh-để-quản-lí-tiến-trình)
      - [A. Câu lệnh ps](#a-câu-lệnh-ps)
      - [B. câu lệnh top](#b-câu-lệnh-top)
      - [C. Công cụ htop](#c-công-cụ-htop)
      - [D. Câu lệnh kill](#d-câu-lệnh-kill)
- [END](#end)




## I. Quản lí dịch vụ

Quản lý dịch vụ trong hệ điều hành Linux là một kỹ năng quan trọng cho việc duy trì và quản lý hệ thống. Dưới đây là giải thích về các thao tác cơ bản như bắt đầu, dừng, khởi động lại dịch vụ, và kiểm tra trạng thái dịch vụ bằng các lệnh ``systemctl`` và ``service``.

>[!WARNING]
>Mọi câu lệnh đều được chạy dưới quyền ``root``, nếu không chạy quyền ``root`` thì thêm ``sudo`` vào trước các câu lệnh. 

### 1. Bắt đầu, dừng, và khởi động lại dịch vụ

Câu lệnh ``systemctl`` là công cụ chính để quản lý dịch vụ trong các hệ thống sử dụng ``systemd``.

Cú pháp cơ bản của câu lệnh systemctl: 

``# systemctl [option] [name_service]``

Dưới đây là một số câu lệnh ``systemctl`` thường dùng
* **Bắt đầu dịch vụ** 

    ``# systemctl start [name_service]``

* **Dừng dịch vụ:**

    ``# systemctl stop [name_service]``

* **Khởi động lại dịch vụ:**

    ``# systemctl restart [name_service]``

* **Khởi động lại dịch vụ nếu có thay đổi cấu hình:**

    ``# systemctl reload [name_service]``

* **Kiểm tra trạng thái dịch vụ:**

    ``# systemctl status [name_service]``

Muốn biết thêm chi tiết về câu lệnh các bạn có thể dùng câu lệnh: ``# systemctl -h`` để vào mục hướng dẫn câu lệnh.

Còn một công cụ nữa là ``service`` tuy là công cụ cũ hơn nhưng vẫn được sử dụng nhiều trên các hệ thông không sử dụng ``systemd``

Cú pháp cơ bản của câu lệnh service: ``# service [name_service] [option]``

### 2. Systemd là gì?

**Systemd** là một trình quản lý hệ thống và dịch vụ cho hệ điều hành Linux. Nó là trình quản lý dịch vụ mặc định trong nhiều bản phân phối Linux bao gồm Ubuntu, Red RHEL, OpenSuse và Arch Linux. Systemd là sự kế thừa của các trình quản lý dịch vụ cũ hơn như System V và Upstart .

Không giống như trình quản lý dịch vụ System V, systemd hiệu quả hơn do khởi động các dịch vụ song song để tăng tốc quá trình khởi động Linux. Một tính năng độc đáo khác của systemd là nó cung cấp dịch vụ theo yêu cầu, tức là nó có thể trì hoãn việc bắt đầu dịch vụ cho đến khi hệ thống cần, điều này giúp cải thiện hiệu suất đáng kể.

Systemd không bị giới hạn trong việc quản lý các quy trình hoặc dịch vụ điều hành mà còn có thể được sử dụng để giám sát mạng, bộ định thời gian chạy (running timer) và hơn thế nữa.

### 3. Thực hành

Sau đây chúng ta sẽ thực hành các câu lệnh ở trên để hiểu rõ hơn về cách quản lí dịch vụ trên Linux 

* **Ta sẽ cài đặt dịch vụ Nginx để thực hiện các câu lệnh liên quan về quản lí dịchv vụ**

    Cập nhật danh sách repository

    ``# apt update``

    ![](/thuctap/img/aptupdate.png)

    Cài đặt Nginx

    ``# apt install nginx``

    ![](/thuctap/img/apt_install_nginx.png)

    Kiểm tra xem đã cài đặt Nginx chưa

    ``# Nginx -v``

    ![](/thuctap/img/nginx_v.png)



* **Kiểm tra trạng thái dịch vụ**

    ``# systemctl status nginx``

    ![](/thuctap/img/systemctl_status.png)


    Ở đây nó sẽ hiện ra một bảng gọi là **trạng thái dịch vụ chi tiết** hoặc **service status output**. Bảng này cung cấp thông tin chi tiết về trạng thái hiện tại của dịch vụ, bao gồm nhiều phần khác nhau như trạng thái hoạt động, PID của tiến trình, thời gian hoạt động, và các nhật ký (logs) gần đây.

    Bảng này gồm có các thành phần:

    | Thành phần | Mô tả |
    |----------|-------|
    |``Nginx.service``|Tên dịch vụ và mô tả|
    |``Loaded;``|Thông tin tải dịch vụ|
    |``Active:``|Trạng thái hoạt động|
    |``Docs:``|Tài liệu liên quan|
    |``Main PID:``|PID chính của dịch vụ|
    |``Tasks:``|Các tiến trình con|
    |``Memory``|Sử dụng bộ nhớ|
    |``CGroup:``|Thông tin CGroup của dịch vụ|
    |``Log``|Ghi lại nhật kí hoạt động của dịch vụ|

* **Dừng dịch vụ**

    ``# systemctl stop nginx``

    ![](/thuctap/img/systemctl_stop.png)

* **Bắt đầu dịch vụ**

    ``# systemctl start nginx``

    ![](/thuctap/img/systemctl_start.png)

* **Khởi động lại dịch vụ**

    ``# systemctl restart nginx``

    ![](/thuctap/img/systemctl_restart.png)


Và đó là mục thực hành để các bạn dễ hiểu hơn về việc quản lí dịch vụ.

## II. Quản lí tiến trình

### 1. Tiến trình là gì?

* Tiến trình (process) là một chương trình đang chạy trong hệ thống. Nó bao gồm mã thực thi(PID), dữ liệu(Memory), và các tài nguyên cần thiết để hoạt động.

* Loại tiến trình:

    1. Tiến trình nền (**Background process**): Chạy mà không cần sự tương tác của người dùng. Thường là các dịch vụ hệ thống như web server, database server, hoặc các tiến trình tự động hóa.

    2. Tiến trình tiền cảnh (**Foreground process**): Chạy và tương tác trực tiếp với người dùng thông qua terminal hoặc GUI. Người dùng có thể nhập lệnh và nhận phản hồi ngay lập tức.

    3. Tiến trình cha (**Parent Process**): Tiến trình tạo ra các tiến trình con. Mỗi tiến trình trong Linux đều có một tiến trình cha (ngoại trừ tiến trình init hoặc systemd, là tiến trình gốc của tất cả các tiến trình).

    4. Tiến trình con (**Child Process**); Được tạo ra bởi một tiến trình khác gọi là tiến trình cha (parent process). Tiến trình con kế thừa nhiều thuộc tính từ tiến trình cha và có thể chạy song song hoặc nối tiếp với tiến trình cha.

    5. Tiến trình zombie (**Zombie Process**): Một tiến trình đã kết thúc nhưng vẫn còn một mục nhập trong bảng tiến trình. Điều này xảy ra khi tiến trình cha chưa đọc trạng thái kết thúc của nó thông qua lệnh ``wait()``.

    6. Tiến trình mồ côi (**Orphan Process**): Tiến trình con mà tiến trình cha đã kết thúc trước khi tiến trình con hoàn thành. Trong trường hợp này, tiến trình mồ côi sẽ được tiếp quản bởi tiến trình ``init`` hoặc ``systemd``.

    7. **Daemon**: Là các tiến trình chạy nền, thường khởi động cùng hệ thống và chạy liên tục. Chúng không tương tác trực tiếp với người dùng và thường thực hiện các tác vụ như quản lý dịch vụ hệ thống.

* Quản lý tiến trình là kỹ năng cơ bản nhưng rất quan trọng trong quản trị hệ thống Linux. Hiểu và sử dụng thành thạo các công cụ và lệnh liên quan sẽ giúp bạn giám sát và kiểm soát hệ thống hiệu quả hơn.
### 2. Các lệnh để quản lí tiến trình

#### A. Câu lệnh ps

* Lệnh ps (``Process Status``) trong Linux là một công cụ hữu ích để hiển thị thông tin về các tiến trình hiện đang chạy trong hệ thống. Nó cung cấp một bản tóm tắt về các tiến trình tại thời điểm lệnh được thực thi. Nó không cập nhật dữ liệu theo thời gian thực mà chỉ hiển thị thông tin tại thời điểm chạy lệnh.

* Câu lệnh ``ps`` thường có cú pháp cơ bản: 

    ``# ps [option]``

    | Option    | Mô tả                                                              |
    |---------------|---------------------------------------------------------------------|
    | `-A`, `-e`    | Liệt kê tất cả các tiến trình trên toàn hệ thống.                   |
    | `-a`          | Liệt kê tất cả các tiến trình ngoại trừ các tiến trình dẫn đầu phiên và không liên kết với TTY. |
    | `-d`          | Liệt kê tất cả các tiến trình ngoại trừ các tiến trình dẫn đầu phiên, cung cấp chế độ xem được lọc. |
    | `--deselect`, `-N` | Liệt kê tất cả các tiến trình ngoại trừ các tiến trình không đáp ứng điều kiện cụ thể. |
    | `-f`          | Hiển thị thứ bậc của các tiến trình dưới dạng ASCII art, minh họa mối quan hệ cha-con. |
    | `-j`          | Hiển thị thông tin chi tiết về tiến trình ở định dạng công việc (job format). |
    | `-T`          | Liệt kê các tiến trình liên quan đến thiết bị đầu cuối hiện tại.    |
    | `-r`          | Chỉ liệt kê các tiến trình đang chạy.                               |
    | `-u`          | Mở rộng đầu ra để bao gồm thông tin chi tiết như mức sử dụng CPU và bộ nhớ. |
    | `-u <user>`   | Liệt kê các tiến trình liên quan đến người dùng cụ thể.             |
    | `-x`          | Bao gồm các tiến trình không có TTY, bao gồm cả các tiến trình nền.  |

    **Bảng thông tin của câu lệnh ``ps``**

    ![](/thuctap/img/ps.png)

    ``PID – ID`` tiến trình duy nhất.

    ``TTY`` – loại thiết bị đầu cuối mà người dùng đăng nhập.

    ``TIME`` – lượng CPU tính bằng phút và giây mà tiến trình đang chạy.

    ``CMD`` – tên của lệnh khởi chạy tiến trình. 

#### B. câu lệnh top

* Lệnh ``top`` tương tự như lệnh ``ps`` là để hiển thị các thông tin về các tiến trình nhưng khác ở chỗ top cung cấp một giao diện đồ họa với cập nhật dữ liệu liên tục về tình trạng các tiến trình và tài nguyên hệ thống. Nó cập nhật dữ liệu trong thời gian thực và cho phép người dùng tương tác để quản lý tiến trình.

* Câu lệnh ``top`` chỉ cần cú pháp: ``# top`` là chạy được.

    ![](/thuctap/img/top.png)

    Thông tin liên quan đến quy trình bao gồm:

    ``PID``: Xử lý ID

    ``USER``: Chủ sở hữu của quá trình

    ``PR``: Sự ưu tiên

    ``NI``: Mức độ ưu tiên

    ``VIRT``: Sử dụng bộ nhớ ảo

    ``RES``: Kích thước cài đặt thường trú (bộ nhớ vật lý không được hoán đổi được sử dụng)

    ``SHR``: Bộ nhớ dùng chung

    ``S``: Trạng thái tiến trình (S: Đang ngủ, R: Đang chạy, I: Không hoạt động)

    ``%CPU``: Phần trăm sử dụng CPU

    ``%MEM``: Phần trăm sử dụng bộ nhớ

    ``TIME+``: Tổng thời gian CPU

    ``COMMAND``: Tên lệnh hoặc tiến trình

#### C. Công cụ htop

* Htop là một công cụ giám sát hệ thống tương tác, trình xem tiến trình và trình quản lý tiến trình được thiết kế cho các hệ thống Unix. Ban đầu được thiết kế như một sự thay thế cho chương trình top trong Unix, nó cung cấp nhiều tính năng tương tự như top nhưng cung cấp khả năng linh hoạt hơn đáng kể trong việc xem các tiến trình hệ thống.

* Khác với top, htop cung cấp danh sách đầy đủ các tiến trình đang chạy thay vì chỉ các tiến trình tiêu tốn tài nguyên cao nhất. Htop có thể hiển thị các tiến trình dưới dạng cây và sử dụng màu sắc để cung cấp thống kê sử dụng tài nguyên.

* Htop đóng ba vai trò chính:

    1. Giám sát hệ thống

    2. Xem tiến trình

    3. Quản lý tiến trình

* **Cài đặt htop**
    
    ![](/thuctap/img/apthtop.png)

    Dùng câu lệnh htop để sử dụng:

    ![](/thuctap/img/menuhtop.png)

#### D. Câu lệnh kill

* Câu lệnh kill trong Linux được sử dụng để kết thúc một tiến trình hoặc một nhóm tiến trình bằng cách gửi một tín hiệu đến các tiến trình đó.

* Cú pháp của nó như sau:

    ``# kill [option] [PID]``

    Lệnh kill sẽ gửi một tín hiệu đến các tiến trình hoặc nhóm tiến trình được chỉ định (PID).

    Các option được sử dụng phổ biến nhất là:
    
    ``1 (HUP)`` - Khởi động lại tién trình.
    
    ``9 (KILL)`` - Dừng tiến trình ngay lập tức.
    
    ``15 (TERM)`` - Dừng quá trình nhẹ nhàng hơn.



# END