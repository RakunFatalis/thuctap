# OpenPanel

# Mục lục

- [OpenPanel](#openpanel)
- [Mục lục](#mục-lục)
- [I. Open Panel](#i-open-panel)
  - [1. Open Panel là gì.](#1-open-panel-là-gì)
  - [2. Ưu và nhược điểm của OpenPanel.](#2-ưu-và-nhược-điểm-của-openpanel)
  - [3. Các gói dịch vụ của OpenPanel:](#3-các-gói-dịch-vụ-của-openpanel)
- [II. Cài đặt OpenPanel](#ii-cài-đặt-openpanel)
  - [1. Yêu cầu cấu hình](#1-yêu-cầu-cấu-hình)
  - [2. Cài đặt OpenPanel](#2-cài-đặt-openpanel)
- [END](#end)


> [!WARNING]
> Lưu ý rằng thông tin trong bài viết này được viết vào ngày **26/10/2024**. Nội dung và tính năng của OpenPanel có thể thay đổi theo thời gian, vì vậy hãy kiểm tra trang thông tin chính thức để có thông tin mới nhất.


# I. Open Panel

## 1. Open Panel là gì.

**OpenPanel** là một bảng điều khiển hosting mạnh mẽ và linh hoạt dành cho hệ thống Linux. OpenPanel có hai phiên bản lựa chọn: một phiên bản được cộng đồng hỗ trợ và một phiên bản cao cấp với nhiều tính năng vượt trội cùng dịch vụ hỗ trợ chuyên nghiệp. 

Điểm nổi bật của OpenPanel so với các bảng điều khiển hosting khác là khả năng cung cấp cho mỗi người dùng một môi trường riêng biệt và các công cụ quản lý đầy đủ. Điều này cho phép người dùng kiểm soát hoàn toàn môi trường của mình, tương tự như khi sử dụng VPS. Bạn có thể dễ dàng cài đặt các phiên bản PHP mới, tùy chỉnh cấu hình máy chủ, xem nhật ký tên miền, khởi động lại các dịch vụ và thực hiện nhiều tác vụ nâng cao khác.

![](/img/CP_OpenPanel_Scheme.png)

Theo nhóm phát triển OpenPanel, bảng điều khiển này là thành quả của nhiều năm kinh nghiệm trong ngành dịch vụ lưu trữ, đã được tích hợp tất cả những tính năng thực sự cần thiết để đáp ứng nhu cầu của người dùng.

Khi họ thiết kế OpenPanel, các tính năng đã được ưu tiên để đảm bảo vừa thân thiện với người mới bắt đầu, vừa đủ mạnh mẽ để giảm bớt công việc bảo trì cho quản trị hệ thống và đội ngũ hỗ trợ lưu trữ.

**Một số tính năng đáng chú ý của OpenPanel bao gồm:**

  + Người dùng có thể chạy máy chủ web **Nginx** hoặc **Apache**.
 
  + Hỗ trợ cả **MySQL** và **MariaDB** cho cơ sở dữ liệu.
 
  + Cho phép người dùng cài đặt các **phiên bản PHP cần thiết**, **chỉnh sửa các tệp php.ini** và thiết lập giới hạn mong muốn.
 
  + **Quản lý cài đặt MySQL**, thiết lập giới hạn, **bật quyền truy cập từ xa** và nhiều tùy chọn khác.
 
  + **Cập nhật các dịch vụ hệ thống** và thậm chí cài đặt các dịch vụ mới theo nhu cầu.
 
  + Quản lý các trang web WordPress dễ dàng thông qua **WP Manager**.
 
  + Đăng nhập không cần mật khẩu vào **phpMyAdmin** và **Web Terminal**.
 
  + Tích hợp **REDIS** và **Memcached** cho việc lưu trữ đối tượng.

## 2. Ưu và nhược điểm của OpenPanel.

**Ưu điểm**

OpenPanel đã nhanh chóng thu hút sự chú ý trong ngành dịch vụ lưu trữ nhờ vào những cải tiến và tính năng nổi bật mà nó mang lại. Với kinh nghiệm nhiều năm trong lĩnh vực này, nhóm phát triển đã nhận diện được nhu cầu thiết thực của người dùng và tạo ra một giải pháp không chỉ tiết kiệm chi phí mà còn linh hoạt và mạnh mẽ. Dưới đây là một số ưu điểm nổi bật của OpenPanel, giúp nó trở thành một lựa chọn lý tưởng cho những ai đang tìm kiếm một bảng điều khiển hosting hiệu quả.

+ **Trải nghiệm giống VPS**

   OpenPanel mang đến cho người dùng trải nghiệm tương tự như VPS nhưng với chi phí thấp hơn. Các tính năng như giới hạn tài nguyên, cách ly người dùng, và quản lý WordPress (WP Manager) được tích hợp, giúp việc lưu trữ trở nên an toàn và dễ dàng hơn.

+ **Giao diện thân thiện**:

  OpenPanel có giao diện dễ sử dụng, thân thiện với người mới, giúp người dùng nhanh chóng làm quen và sử dụng các tính năng mà không gặp khó khăn.

+ **Tính tùy chỉnh linh hoạt**:

  OpenPanel là bảng điều khiển mô-đun đầu tiên thực sự cho phép mọi thứ được tùy chỉnh và hoạt động độc lập với phần còn lại của hệ thống. Nó cũng không phụ thuộc vào hệ điều hành và hoạt động giống nhau trên tất cả các hệ thống được hỗ trợ.

**Nhược điểm**

  Do là OpenPanel mới ra mắt vào thời gian gần đây nên vẫn còn một số hạn chế nhất định.

  + **Hỗ trợ cộng đồng còn hạn chế:**
  
    Mặc dù có một cộng đồng hỗ trợ, nhưng không phát triển mạnh như một số panel hosting khác, điều này có thể gây khó khăn trong việc tìm kiếm giải pháp cho các vấn đề phát sinh.

  + **Tính ổn định:**
    
    OpenPanel vẫn đang trong quá trình hoàn thiện, có thể gặp một số vấn đề về ổn định khi sử dụng, đặc biệt là với các tính năng mới

  + **Chưa phổ biến với đại đa số người dùng:**
   
    OpenPanel vẫn đang trong giai đoạn phát triển và chưa được nhiều người dùng biết đến hoặc sử dụng rộng rãi, điều này có thể ảnh hưởng đến sự tin cậy và hỗ trợ từ cộng đồng.

  + **Không phải mã nguồn mở:** 
  
    Mặc dù cái tên "**OpenPanel**" có thể khiến nhiều người nhầm tưởng rằng đây là một dự án mã nguồn mở, nhưng thực tế nhóm phát triển đã cân nhắc việc mã nguồn mở và quyết định không theo đuổi con đường này. Quyết định này có thể làm giảm sự linh hoạt và khả năng tùy chỉnh cho những ai mong muốn can thiệp vào mã nguồn.

## 3. Các gói dịch vụ của OpenPanel:

**Community Edition:**

Đây là một bảng điều khiển hosting miễn phí cho tối đa 3 tài khoản người dùng. Phiên bản này phù hợp cho người dùng cá nhân hoặc VPS, cho những ai cần quản lý nhỏ mà không tốn phí.

**Enterprise Edition:**

Đây là phiên bản cao cấp cung cấp các tính năng nâng cao cho việc cách ly và quản lý người dùng.  Phiên bản này lý tưởng cho các nhà cung cấp dịch vụ lưu trữ web, những người cần các công cụ mạnh mẽ hơn để quản lý tài nguyên và người dùng.

# II. Cài đặt OpenPanel


## 1. Yêu cầu cấu hình

Để cài đặt được OpenPanel, các bạn cần đáp ứng những yêu cầu tối thiểu sau:

+ **Máy chủ ảo hoặc máy chủ vật lý**: Cần có một máy chủ ảo hoàn toàn trống hoặc máy chủ vật lý.

+ **Bộ nhớ và lưu trữ**: Tối thiểu 1GB RAM và 15GB dung lượng lưu trữ (khuyến nghị 4GB RAM và 50GB dung lượng lưu trữ).

**Kiến trúc**: Cần sử dụng kiến trúc x86_64/amd64.

+ **Địa chỉ IPv4**: Cần có một địa chỉ IPv4 để hoạt động.

Hệ điều hành OpenPanel hỗ trợ:

+ AlmaLinux 9.4
+ Fedora 40
+ RockyLinux 9.4
+ CentOS 9+ 
+ Ubuntu 22 and 24
+ Debian 11 and 12

Nếu bạn đang sử dụng tường lửa bên ngoài, bạn nên đảm bảo rằng các cổng sau được mở để cho phép giao tiếp cần thiết:

  ``53``|``80``|``443``|``465``|``2083``|``2087``|``32768:60999``
## 2. Cài đặt OpenPanel

Để bắt đầu bạn hãy ``ssh`` tới VPS hoặc máy chủ của các bạn với quyền ``root`` để bắt đầu cài đặt.

        # ssh root@ip_VPS_của_bạn -p port_truy_cập

Các bạn nên cập nhật hệ thống của mình trước khi cài đặt OpenPanel

Dành cho hệ điều hành Ubuntu:
        
        # apt update && apt upgrade -y

Dành cho hệ điều hảnh Centos:

        # yum update && yum upgrade -y


Cài đặt các gói cần thiết như wget và curl.

Dành cho hệ điều hành Ubuntu:

        # apt install wget curl -y

Dành cho hệ điều hành Centos:

        # yum install wget curl -y

Sau khi đã cập nhật xong tất cả, các bạn vào trang web của OpenPanel để lấy script cài đặt. Các bạn hãy vào bằng đường link này: **https://openpanel.com/docs/admin/intro/#installation**

![](/img/CP_OpenPanel_Script_Web.png)

Dành cho những bạn không vào được đường dẫn trang web thì đây là script tự động cài đặt OpenPanel:

        # bash <(curl -sSL https://openpanel.org)

![](/img/CP_OpenPanel_RunScript.png)

Khi cài đặt xong thì hệ thống sẽ cung cấp thông tin tài khoản và mật khẩu để bạn đăng nhập.

![](/img/CP_OpenPanel_Infor.png)

Trang đăng nhập OpenPanel.

![](/img/CP_OpenPanel_LoginPage.png)

Trang dashboard admin OpenPanel

![](/img/CP_OpenPanel_AdminDashboard.png)

Và thế là hoàn tất, giờ bạn có thể bắt đầu sử dụng OpenPanel để quản trị các website của mình.

# END