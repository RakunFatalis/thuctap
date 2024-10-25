# CyberPanel

# Mục lục

- [CyberPanel](#cyberpanel)
- [Mục lục](#mục-lục)
- [I. Cài đặt CyberPanel](#i-cài-đặt-cyberpanel)
- [II. Cài đặt website và SSL](#ii-cài-đặt-website-và-ssl)
  - [1. Cài đặt website trên CyberPanel](#1-cài-đặt-website-trên-cyberpanel)
  - [2. Cài đặt SSL](#2-cài-đặt-ssl)
- [END](#end)

# I. Cài đặt CyberPanel

Bạn hãy ``ssh`` tới VPS của các bạn với quyền ``root`` để bắt đầu cài đặt.

        # ssh root@ip_VPS_của_bạn -p port_truy_cập

Các bạn nên cập nhật hệ thống của mình trước.

        # apt update && apt upgrade -y

Cài đặt các gói cần thiết như wget và curl.

        # apt install wget curl -y

Sau khi đã setup xong tất cả, các bạn vào trang web của CyberPanel để lấy script cài đặt. Các bạn hãy vào bằng đường link này: **https://community.cyberpanel.net/t/01-installing-cyberpanel/82**

![](/thuctap/img/CP_CyberPanel_Script.png)

Đoạn script cài đặt:

        sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)

Khi chạy script này thì hệ thống sẽ yêu cầu trả lời một số câu hỏi.

Tại đây bạn chon 1 để cài đặt CyberPanel.

![](/thuctap/img/CP_CyberPanel_Q1.png)

Tiếp theo sẽ có lựa chọn cài LiteSpeed cho các bạn.

1. **Install CyberPanel with OpenLiteSpeed:** Đây là lựa chọn sử dụng OpenLiteSpeed, một phiên bản mã nguồn mở và miễn phí của LiteSpeed Web Server.

2. **Install CyberPanel with LiteSpeed Enterprise:** Đây là phiên bản trả phí của LiteSpeed, cung cấp nhiều tính năng hơn so với OpenLiteSpeed, đặc biệt là các tính năng dành cho hiệu suất cao, tăng cường bảo mật, và hỗ trợ khách hàng chuyên nghiệp. Bạn sẽ cần có giấy phép sử dụng LiteSpeed Enterprise.

Tại đây mình chọn 1.

![](/thuctap/img/CP_CyberPanel_Q2.png)

Tiếp theo là cài đặt các tiện ích bổ sung. Tại đây các bạn nhập **Y** để cài đặt

![](/thuctap/img/CP_CyberPanel_Q3.png)

Kế tiếp hệ thống sẽ hỏi bạn là có muốn remote database của các bạn không. Tại đây mình chọn "**N**".

![](/thuctap/img/CP_CyberPanel_Q4.png)

Hệ thống sẽ hỏi bạn muốn cài đặt Cyberpanel phiên bản nào. Tại đây các bạn nhập phiên bản các bạn muốn tải hoặc nhấn "**Enter**" để cài đặt phiên bản mới nhất.

![](/thuctap/img/CP_CyberPanel_Q5.png)

Trong thông báo này, bạn có các tùy chọn sau để cài đặt mật khẩu admin cho CyberPanel:

    
    [d]efault: Sử dụng mật khẩu mặc định là 1234567.
    
    [r]andom: Tạo mật khẩu ngẫu nhiên (được khuyến nghị).
    
    [s]et password: Đặt mật khẩu theo ý bạn.

Bạn nên chọn [r]andom để tạo mật khẩu an toàn hơn.

![](/thuctap/img/CP_CyberPanel_Q6.png)

Sau khi chọn mật khẩu xong các bạn sẽ được hỏi có cài đặt các tiện ích sau.

   * **Memcached**: Đây là một hệ thống lưu trữ đối tượng phân tán trong bộ nhớ cache. Nó giúp tăng tốc độ tải các trang web bằng cách giảm truy vấn cơ sở dữ liệu.

   * **Redis**: Là một kho lưu trữ cấu trúc dữ liệu trong bộ nhớ, có thể được sử dụng làm cơ sở dữ liệu, bộ nhớ đệm, hoặc hệ thống truyền tải thông điệp. Tương tự như Memcached nhưng có nhiều tính năng hơn.

   * **Watchdog:** Là một dịch vụ hệ thống giám sát hệ thống đang chạy. Nếu phát hiện lỗi phần mềm không thể khắc phục, Watchdog sẽ tự động khởi động lại hệ thống. 
 
![](/thuctap/img/CP_CyberPanel_Q7.png)

Khi đã hoàn thành các bước trên thì hệ thống sẽ cài Cyberpanel, quá trình này sẽ mất 5-10 phút.

Một khi hoàn tất thì hệ thống sẽ cung cấp các thông tin tài khoản cho bạn. Các bạn cần restart hệ thống để áp dụng các cấu hình.

![](/thuctap/img/CP_Cyberpanel_Infor.png)

![](/thuctap/img/CP_Cyberpanel_LoginPage.png)

# II. Cài đặt website và SSL

## 1. Cài đặt website trên CyberPanel

Để cài đặt website của bạn lên Cyberpanel, trong trang dashboard của cyberpanel các bạn click vào ô "**WEBSITES**".

![](/thuctap/img/CP_Cyberpanel_WEBSITES.png)

Sau khi đã chuyển tới trang quản lí website thì các bạn click vào ô "**CREATE WEBSITE**".

![](/thuctap/img/CP_Cyberpanel_WEBSITES_Create.png)

Kế tiếp nó sẽ chuyển tới trang điền thông tin để tạo website dựa trên tên miền của các bạn. Bạn có thể tuỳ chọn có muốn tạo mail domain hay không.

![](/thuctap/img/CP_Cyberpanel_WEBSITES_Create_Infor.png)

![](/thuctap/img/CP_Cyberpanel_WEBSITES_Create_Setup.png)

Để kiểm tra xem website đã được tạo chưa thì các bạn vào tên miền mà website của bạn đã được liên kết vào.

![](/thuctap/img/CP_Cyberpanel_WEBSITES_Check.png)

Hoặc các bạn vào có thể kiếm tra trong "**WEBSITE**" -> "**List Website**".

![](/thuctap/img/CP_Cyberpanel_WEBSITES_ListWeb.png)

* **Upload mã nguồn website.**

Để upload mã nguồn website của các bạn lên, các bạn vào trong  "**WEBSITES**" -> "**List Webstie**" -> "**Manage**"

![](/thuctap/img/CP_Cyberpanel_WEBSITES_ListWeb_Manage.png)

Trong trang manage của website, các bạn kéo xuống kiếm cho mình "**FILES**" -> "**File Manager**"

![](/thuctap/img/CP_Cyberpanel_WEBSITES_ListWeb_Manage_Filemanage.png)

Các bạn vào trong thư mục **public_html** và click vào Upload để tải mã nguồn của các bạn lên.

![](/thuctap/img/CP_Cyberpanel_Public_html.png)

![](/thuctap/img/CP_Cyberpanel_Public_html_Upload.png)


## 2. Cài đặt SSL

Cyberpanel đã tự động cài SSL bằng Let's Encrypt khi bạn cài đặt website cho bạn, còn nếu như trong quá trình cài đặt mà xảy ra một số lỗi gì đó khiến website của bạn không được cài đặt bởi cyberpanel các bạn có thể làm theo cách sau.

Trong trang dashboard, các bạn click vào ô "**SSL**" để vào trang SSL.

![](/thuctap/img/CP_Cyberpanel_SSL.png)

Các bạn click vào ô **MANAGE SSL**.

![](/thuctap/img/CP_CYberpanel_SSL_Manage.png)

Các bạn click vào ô "Issue SSL" để Cyberpanel dùng Let's Encrypt để cài đặt SSL cho website đã chọn của các bạn

![](/thuctap/img/CP_Cyberpanel_SSL_Issue.png)


# END