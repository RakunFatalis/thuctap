# aaPanel

# Mục lục

- [aaPanel](#aapanel)
- [Mục lục](#mục-lục)
- [I. Cài đặt FastPanel](#i-cài-đặt-fastpanel)
- [II. Cài đặt website, SSL lên FastPanel](#ii-cài-đặt-website-ssl-lên-fastpanel)
  - [1. Cài đặt website](#1-cài-đặt-website)
  - [2. Cài đặt SSL cho website](#2-cài-đặt-ssl-cho-website)
- [END](#end)

# I. Cài đặt FastPanel

Bạn hãy ``ssh`` tới VPS của các bạn với quyền ``root`` để bắt đầu cài đặt.

        # ssh root@ip_VPS_của_bạn -p port_truy_cập

Các bạn nên cập nhật hệ thống của mình trước.

        # apt update && apt upgrade -y

Cài đặt các gói cần thiết như wget và curl.

        # apt install wget curl -y

Sau khi đã setup xong tất cả, các bạn vào trang web của FastPanel để lấy script cài đặt. Các bạn hãy vào bằng đường link này: **https://kb.fastpanel.direct/quick_start/how-to-install-fastpanel/**

![](/thuctap/img/CP_FastPanel_Script.png)

Đoạn script cài đăt:

        # wget http://repo.fastpanel.direct/install_fastpanel.sh -O - | bash -

![](/thuctap/img/CP_FastPanel_Script_Run.png)

FastPanel sẽ tự động cài đặt các web service cho bạn và cung cấp cho bạn địa chỉ đăng nhập và tài khoản mật khẩu để đăng nhập.

# II. Cài đặt website, SSL lên FastPanel

## 1. Cài đặt website

Trong giao diện của FastPanel để cài đặt một website các bạn click vào "**Create site**".

![](/thuctap/img/CP_FastPanel_CreateSite.png)

Tại đây bạn có hai lựa chọn:

  1. **Create a CMS based site:** Các bạn tạo lập và quản lý một trang web với hệ thống quản lý nội dung CMS, tại đây là Wordpress

  2. **Create a site manually:** Các bạn tạo một trang web bằng cách thủ công.

![](/thuctap/img/CP_FastPanel_Create_Option.png)

Mình sẽ làm bằng cách thủ công trước.

Đầu tiên FastPanel sẽ yêu cầu các bạn nhập thông tin trong mục Domain binding:

  1. **Which domain to bind?**: Domain mà FastPanel sẽ bind tới.
  
  2. **To which IP address?**: Địa chỉ IP mà Domain sẽ liên kết.
  
  3. **DNS account**: Lựa chọn có tạo DNS account hay không.

![](/thuctap/img/CP_FastPanel_Domainbinding.png)

Phần tiếp theo là phần "**Configuration**", tại đây các bạn cấu hình các mục User, Database, Backend,...

![](/thuctap/img/CP_Fastpanel_Configuration.png)

Sau khi đã cấu hình xong các bạn ấn creatsite là các bạn đã tạo được 1 trang web thủ công.

![](/thuctap/img/CP_Fastpanel_Create_Site_Done.png)

![](/thuctap/img/CP_Fastpanel_Create_Site_Done2.png)

Đó là chỉ mới tạo một trang web cơ bạn, nếu các bạn đã có mã nguồn một trang web thì bước tiếp theo sau đây là cách để bạn up mã nguồn của các bạn lên FastPanel.

* **Upload mã nguồn lên FastPanel**

Để upload mã nguồn của các bạn, các bạn click vào site mà các bạn muốn upload mã nguồn của các bạn lên.

![](/thuctap/img/CP_Fastpanel_choose_site.png)

Trong phần site card của tên miền các bạn, các bạn kéo chuột để kiếm tới phần "Files".

![](/thuctap/img/CP_Fastpanel_Files.png)

Khi đã vào trong trang Files thì các bạn up mã nguồn các bạn lên trên đó.

![](/thuctap/img/CP_Fastpanel_Upload_File.png)

![](/thuctap/img/CP_Fastpanel_checkstie.png)

## 2. Cài đặt SSL cho website

Để cài đặt SSL cho website trong trang site card các bạn kéo xuống kiếm phần **SSL certificates**.

![](/thuctap/img/CP_Fastpanel_SSL.png)

Trong danh sách SSL các bạn click vào ô "**New certificate**" để tạo một SSL cho website

![](/thuctap/img/CP_FastPanel_SSL_new.png)

Tại đây có 4 lựa chọn cho bạn:

1. Sử dụng **Let's Encrypt** để cài đặt SSL miễn phí và sẽ được tự động gia hạn.

2. Sử dụng **Self-signed (Chứng chỉ tự ký)** để cài đặt SSL tuy nhiên vì đây là chứng chỉ tự kí nên nó không được công nhận bởi các trình duyệt chính thống, chứng chỉ này chỉ phù hợp cho môi trường nội bộ hoặc thử ngiệm

3. Sử dụng **Existing (Chứng chỉ có sẵn)** nếu các bạn đã mua SSL từ các nhà cung cấp thì cac1 bạn có thể điền thông tin SSL đó để áp vào website của các bạn

4. **Certificate Signing Request (CSR)** đây là lựa chọn khi bạn có nhu cầu muốn mua SSL từ một nhà cung cấp bên ngoài nhưng chưa có chứng chỉ, bạn cần tạo một yêu cầu ký chứng chỉ (CSR).

![](/thuctap/img/CP_FastPanel_SSL_4Option.png)

Mình sẽ sử dụng Let's Encrypt để cài đặt SSL cho website của mình. Hình ảnh bên dưới là kết quả cài đặt SSL của mình lên website

![](/thuctap/img/CP_Fastpanel_SSL_Done.png)


# END