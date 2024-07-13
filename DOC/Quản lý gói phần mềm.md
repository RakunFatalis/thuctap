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

    Là một công cụ dòng lệnh để quản lý gói phần mềm. Nó sử dụng APT (Advanced Package Tool), một hệ thống quản lý gói phần mềm mạnh mẽ. apt-get có thể tự động tải về, cài đặt, gỡ bỏ, và nâng cấp các gói phần mềm từ các kho lưu trữ phần mềm.

    Câu lệnh của apt-get không khác gì nhiều với apt chỉ cần thay từ ``apt`` thành ``apt-get``

  * **DPKG**

    Là một công cụ cấp thấp hơn, chuyên dùng để quản lý các gói .deb. Nó không có khả năng tự động xử lý phụ thuộc (dependencies) như apt-get. Tuy nhiên, dpkg vẫn rất hữu ích khi bạn cần cài đặt hoặc gỡ bỏ một gói .deb cụ thể mà không cần đến các kho lưu trữ.

    Một số câu lệnh thường dùng của DPKG:

    Câu lệnh cơ bản: # dpks [option] [name.deb]

    | Lệnh                       | Mô tả                                                 |
    |----------------------------|--------------------------------------------------------|
    | `-i`| Cài đặt một gói `.deb`.                                |
    | `-r`| Gỡ bỏ một gói đã cài đặt.                              |
    | `-l`| Liệt kê tất cả các gói đã cài đặt.                     |
    | `-s`| Hiển thị thông tin về một gói đã cài đặt.              |
    | `-L`| Hiển thị danh sách các file thuộc về một gói đã cài đặt. |
  