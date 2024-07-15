# QUẢN LÍ GÓI PHẦN MỀM

# MỤC LỤC
- [QUẢN LÍ GÓI PHẦN MỀM](#quản-lí-gói-phần-mềm)
- [MỤC LỤC](#mục-lục)
  - [I. Quản lý gói phần mềm với APT](#i-quản-lý-gói-phần-mềm-với-apt)
    - [1. Giới thiệu về APT](#1-giới-thiệu-về-apt)
    - [2. Một số lệnh cơ bản của APT](#2-một-số-lệnh-cơ-bản-của-apt)
    - [3. Thực hành](#3-thực-hành)
    - [4. Apt-get và dpkg](#4-apt-get-và-dpkg)
  - [II. Quản lý gói phần mềm với YUM/RPM](#ii-quản-lý-gói-phần-mềm-với-yumrpm)
    - [1. Giới thiệu về YUM/RPM](#1-giới-thiệu-về-yumrpm)
    - [2. Một số lệnh cơ bản của của YUM](#2-một-số-lệnh-cơ-bản-của-của-yum)
- [END](#end)



## I. Quản lý gói phần mềm với APT

### 1. Giới thiệu về APT

Advanced Packaging Tool, hay APT, là phần mềm miễn phí dùng để quản lý việc cài đặt phần mềm trên Linux. APT làm đơn giản các thủ tục quản lý phần mềm trên các máy tính tựa Unix bằng cách tự động hóa việc tải về, cấu hình và cài đặt các gói phần mềm, cả ở dạng biên dịch sẵn (dạng binary) hoặc biên dịch mã nguồn.

APT ban đầu được thiết kế như là một giao diện cho dpkg để làm việc với các gói .deb của Debian, nhưng nó cũng đã được thay đổi để có thể làm việc với hệ thống RPM thông qua apt-rpm. Dự án Fink đã chuyển APT lên hệ điều hành Mac OS X với một số chức năng quản lý gói, và APT cũng đã có trên OpenSolaris (bao gồm bản phân phố Nexenta OS).

### 2. Một số lệnh cơ bản của APT

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

    ![](/img/aptupdate.png)

* **Cài đặt htop:**

    ``# apt install htop``

    ![](//img/apthtop.png)

* **Kiểm tra htop đã được cài đặt chưa** 

    ``# apt list htop``

    ![](/img/checkhtop.png)

* **Xoá gói htop**

    ``# apt remove htop``

    ![](//img/removehtop.png)

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

## II. Quản lý gói phần mềm với YUM/RPM

  ### 1. Giới thiệu về YUM/RPM

* YUM (Yellowdog Updater, Modified) là một công cụ quản lý gói phần mềm cho các hệ điều hành dựa trên Linux, chủ yếu là CentOS, Fedora, và Red Hat Enterprise Linux (RHEL). Dưới đây là một bản giới thiệu về YUM:

  YUM là một trình quản lý gói phần mềm mạnh mẽ trên các hệ điều hành Linux, được phát triển để đơn giản hóa việc quản lý cài đặt và nâng cấp phần mềm. Nó cho phép người dùng dễ dàng tải về, cài đặt, cập nhật và loại bỏ các gói phần mềm trên hệ thống một cách an toàn và hiệu quả.

* RPM (Red Hat Package Manager) là hệ thống quản lý gói phần mềm chính cho các hệ điều hành dựa trên Linux, được phát triển ban đầu bởi Red Hat và hiện đã trở thành một tiêu chuẩn trong việc quản lý phần mềm trên các bản phân phối như CentOS, Fedora, và Red Hat Enterprise Linux (RHEL).

  ### 2. Một số lệnh cơ bản của của YUM

| Lệnh YUM | Mô tả |
|----------|-------|
| `yum install <tên_gói>` | Cài đặt gói phần mềm từ kho lưu trữ YUM. |
| `yum remove <tên_gói>` | Xoá gói phần mềm khỏi hệ thống. |
| `yum update` | Cập nhật tất cả các gói phần mềm đã được cài đặt lên phiên bản mới nhất. |
| `yum upgrade` | Cập nhật các gói phần mềm lên phiên bản mới nhất và tự động giải quyết các phụ thuộc. |
| `yum search <từ_khóa>` | Tìm kiếm gói phần mềm trong các kho lưu trữ YUM. |
| `yum info <tên_gói>` | Hiển thị thông tin chi tiết về một gói phần mềm cụ thể. |
| `yum list installed` | Liệt kê tất cả các gói phần mềm đã được cài đặt trên hệ thống. |
| `yum clean packages` | Xóa các gói phần mềm đã được tải về và lưu trữ trong bộ nhớ cache của YUM. |
| `yum clean all` | Xóa tất cả các dữ liệu cache của YUM, bao gồm cả metadata và gói phần mềm đã tải về. |


| Lệnh RPM | Mô tả |
|----------|-------|
| `rpm -i <tên_file.rpm>` | Cài đặt gói phần mềm từ file .rpm đã tải về. |
| `rpm -e <tên_gói>` | Xoá gói phần mềm khỏi hệ thống. |
| `rpm -q <tên_gói>` | Kiểm tra xem gói phần mềm đã được cài đặt hay chưa và phiên bản hiện tại. |
| `rpm -U <tên_file.rpm>` | Nâng cấp gói phần mềm đã có sẵn lên phiên bản mới từ file .rpm. |
| `rpm -F <tên_file.rpm>` | Nâng cấp chỉ các tệp đã có sẵn trong hệ thống lên phiên bản mới từ file .rpm. |
| `rpm -qa` | Liệt kê tất cả các gói phần mềm đã được cài đặt trên hệ thống. |
| `rpm -qi <tên_gói>` | Hiển thị thông tin chi tiết về một gói phần mềm cụ thể đã được cài đặt. |
| `rpm -ql <tên_gói>` | Liệt kê các tệp tin được cài đặt bởi gói phần mềm. |
| `rpm -qf <đường_dẫn/tệp_tin>` | Tìm kiếm gói phần mềm mà tệp tin thuộc về. |
| `rpm -Uvh <tên_file.rpm>` | Cài đặt hoặc nâng cấp gói phần mềm từ file .rpm và hiển thị tiến trình chi tiết. |

# END
