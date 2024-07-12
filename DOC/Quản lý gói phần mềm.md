# QUẢN LÍ GÓI PHẦN MỀM

# MỤC LỤC



## I. Quản lý gói phần mềm với APT

### 1. Giới thiệu về APT

Advanced Packaging Tool, hay APT, là phần mềm miễn phí dùng để quản lý việc cài đặt phần mềm trên Linux. APT làm đơn giản các thủ tục quản lý phần mềm trên các máy tính tựa Unix bằng cách tự động hóa việc tải về, cấu hình và cài đặt các gói phần mềm, cả ở dạng biên dịch sẵn (dạng binary) hoặc biên dịch mã nguồn.

APT ban đầu được thiết kế như là một giao diện cho dpkg để làm việc với các gói .deb của Debian, nhưng nó cũng đã được thay đổi để có thể làm việc với hệ thống RPM thông qua apt-rpm. Dự án Fink đã chuyển APT lên hệ điều hành Mac OS X với một số chức năng quản lý gói, và APT cũng đã có trên OpenSolaris (bao gồm bản phân phố Nexenta OS).

### 2. Một số lệnh quan trong của APT

| Lệnh | Mô tả |
|----------|-------|
|``apt install <tên_gói>``|Cài đặt gói|
|``apt remove <tên_gói>`` |Xoá gói    |
|``apt purge <tên_gói>``  |Xóa gói cùng với cấu hình |
|``apt update``           |Cập nhật danh sách gói |
|``apt upgrade``          |Cập nhật gói|
|``apt full-upgrade``     |Cập nhật và nâng cấp gói|
|``apt search <từ_khóa>`` |Tìm kiếm gói|
|``apt show <tên_gói>``   |Hiển thị thông tin chi tiết về gói|
|``apt autoremove``       |Xóa các gói không còn dùng đến|
|``apt clean``            |Xóa các gói cache đã tải về|

### 3. Thực hành

* **Cập nhật danh sách gói:**

    ``# apt update``

    ![](/thuctap/img/aptupdate.png)

* **Cài đặt htop:**

    ``# apt install htop``

    ![](/thuctap//img/apthtop.png)

* **Kiểm tra htop đã được cài đặt chưa** 

    ``# apt list htop``

    ![](/thuctap/img/checkhtop.png)

* **Xoá gói htop**

    ``# apt remove htop``

    ![](/thuctap//img/removehtop.png)

### 4. Apt-get và dpkg

  * **Apt-get**
  