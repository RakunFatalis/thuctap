# VestaCP

# Mục lục

- [VestaCP](#vestacp)
- [Mục lục](#mục-lục)
- [I. Cài đặt VestaCP](#i-cài-đặt-vestacp)
- [II. Cài đặt website và cái chứng chỉ SSL](#ii-cài-đặt-website-và-cái-chứng-chỉ-ssl)
- [END](#end)

# I. Cài đặt VestaCP

Bạn hãy ``ssh`` tới VPS của các bạn với quyền ``root`` để bắt đầu cài đặt.

        # ssh root@ip_VPS_của_bạn -p port_truy_cập

Các bạn nên cập nhật hệ thống của mình trước.

        # apt update && apt upgrade -y

Cài đặt các gói cần thiết như wget và curl.

        # apt install wget curl -y

Sau khi đã setup xong tất cả, các bạn vào trang web của VestaCP để lấy script cài đặt. Các bạn hãy vào bằng đường link này: **https://vestacp.com/install#install-configure**

Trong trang web vestaCP, các bạn hãy lựa chọn những dịch vụ mà bạn muốn cài với vesta rồi sau đó ấn vào ô "**Generate Install Command**" để trang web tạo script cài đặt cho bạn

![](/thuctap/img/CP_Vesta_Generate_Script.png)

![](/thuctap/img/CP_Vesta_Script.png)

Còn nếu bạn không muốn phức tạp thì chỉ muốn tải vestaCP thôi thì chỉ cần chạy lệnh này sau lệnh curl:

        bash vst-install.sh

Sau khi đã chạy lệnh thì hệ thống sẽ báo rằng vesta sẽ cài đặt các tiện ích phục vụ. Tại đây các bạn nhấn "**Y**", quá trình này sẽ mất khoảng 15 phút.

![](/thuctap/img/CP_Vesta_run_Script.png)

![](/thuctap/img/CP_Vesta_Download.png)

# II. Cài đặt website và cái chứng chỉ SSL

Để tạo một website, các bạn vào phần "**Web**" của VestaCP và click vào dấu cộng.

![](/thuctap/img/CP_Vesta_Website_Create.png)

Tại đây các bạn điền tên miền của các bạn vào tích những support mà website bạn cần.

![](/thuctap/img/CP_Vesta_Website_Infor.png)

Trong phần "**Advanced options**", có tuỳ chọn cài đặt SSL cho website của bạn. Nếu bạn đã có SSL thì copy chứng chỉ SSL đó vào, nếu không có các bạn có thể tích chọn dùng Let's Encrypt để cài đặt chứng chỉ SSL miễn phí. 

> [!WARNING]
> Lưu ý là SSL được tạo bởi Let's Encrypt sẽ tự động cài lên sau khoảng 5 phút

![](/thuctap/img/CP_Vesta_Website_Infor2.png)

![](/thuctap/img/CP_Vesta_Website_Infor3.png)
* **Upload mã nguồn website lên**

Trước khi bắt đầu thì VestaCP về cơ bản thì nó không có tích hợp sẵn FILE MANAGER khi cài đặt. Để kích hoạt FILE MANAGER lên các bạn làm theo cách sau.

Các bạn truy cập SSH với quyền root vào máy chủ các bạn và bật terminal lên.

  * **Chỉnh sửa file cấu hình VestaCP:**
  
        # nano /usr/local/vesta/conf/vesta.conf
    
    Các bạn thêm dòng này vào trong file cấu hình VestaCP:

        FILEMANAGER_KEY='FREEFM'

    Các bạn khởi động lại dịch vụ VestaCP và đăng nhập lại Vesta.

        # systemctl restart vesta

    ![](/thuctap/img/CP_Vesta_Filemanager.png)

Giờ các bạn có thể upload mã nguồn các bạn lên website.

Để upload mã nguồn thì các bạn vào File Manager. Sau đó các bạn vào thư mục "**web**" -> "**Website bạn vừa tạo**" -> "**public_html**" để upload mã nguồn lên.

![](/thuctap/img/CP_Vesta_File.png)

Các bạn click vào ô "**UPLOAD**" để tải mã nguồn của các bạn lên.

![](/thuctap/img/CP_Vesta_Upload_file.png)



















# END