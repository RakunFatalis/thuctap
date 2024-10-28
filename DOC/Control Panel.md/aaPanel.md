# aaPanel

# Mục lục

- [aaPanel](#aapanel)
- [Mục lục](#mục-lục)
- [I. Cách cài đặt aaPanel](#i-cách-cài-đặt-aapanel)
- [II. Cài đặt website, SSL lên các control panel](#ii-cài-đặt-website-ssl-lên-các-control-panel)
  - [1. Cài đặt website](#1-cài-đặt-website)
  - [2. Cài đặt SSL cho trang web](#2-cài-đặt-ssl-cho-trang-web)
- [END](#end)



# I. Cách cài đặt aaPanel


Bạn hãy ``ssh`` tới VPS của các bạn với quyền ``root`` để bắt đầu cài đặt.

        # ssh root@ip_VPS_của_bạn -p port_truy_cập

Các bạn nên cập nhật hệ thống của mình trước.

        # apt update && apt upgrade -y

Cài đặt các gói cần thiết như wget và curl.

        # apt install wget curl -y

Sau khi đã setup xong tất cả, các bạn vào trang web của aaPanel để lấy script cài đặt. Các bạn hãy vào bằng đường link này: **https://www.aapanel.com/new/download.html#install**

![](/img/CP_aaPanel_Script.png)

Đoạn script cài đặt aaPanel:

    # URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel

Các bạn nhấn Y để đồng ý cài đặt.

![](/img/CP_aaPanel_Script_Copy.png)

Sau khi hoàn tất quá trình cài đặt aaPanel thì hệ thống cũng sẽ cung cấp luôn địa chỉ ip để đăng nhập và thông tin tài khoản đăng nhập cho các bạn.

![](/img/CP_aaPanel_infoLogin.png)

Nếu các bạn không truy cập được địa chỉ ip thì nên kiểm tra tường lửa có chặn các cổng kết nối của aaPanel không.

![](/img/CP_aaPanel_install_success.png)


# II. Cài đặt website, SSL lên aaPanel

## 1. Cài đặt website

Khi cài đặt xong thì aaPanel sẽ cho bạn lựa chọn cài đặt LNMP stack hay LAMP stack, mỗi lựa chọn cài đặt đều có hai phương phức cài đặt.

* **Fast**: sử dụng rpm, được cài đặt trong thời gian rất ngắn (khoảng 5~10 phút), với hiệu suất và độ ổn định thấp hơn một chút so với phiên bản đã biên dịch."

* **Compiled**: Được cài đặt trong thời gian dài (từ 30 phút đến 3 giờ), phù hợp cho môi trường sản xuất.

Tại đây mình sẽ chọn cài đặt LNMP stack với phương thức tải Fast.

![](/img/CP_aapanel_LNMP.png)
![](/img/CP_aapanel_LNMP_install.png)

Sau khi đã cài đặt xong các bạn vào phần "**Website**" và click vào ô "**Add site**" để thêm tên miền của các bạn.

![](/img/CP_aaPanel_Addsite.png)

![](/img/CP_aaPanel_Addsite_Infor1.png)

![](/img/CP_aaPanel_Addsite_Infor2.png)

![](/img/CP_aaPanel_Website_success.png)
Cũng trong phần "**Website**", các bạn click vào đường dẫn chứa thư mục mã nguồn website của các bạn tại cột "**Document Root**" để chuyển sang trang quản lí tệp tin tại thư mục root.

![](/img/CP_aaPanel_Docroot.png)

Trong trang quản lí tệp tin của các bạn hãy click vào ô "**Upload**" để tải mã nguồn các bạn lên.

![](/img/CP_aaPanel_Upload.png)

Sau khi đã upload xong mã nguồn thì các bạn vào tên miền của các bạn để kiểm tra xem website đã được hoạt động chưa.

**Nếu các bạn muốn dùng địa chỉ IP để truy cập website của mình thì hãy làm theo các bước sau đây.**

Các bạn vào phần "**Website**" và hãy click vào ô "**Default Website**"

![](/img/CP_aaPanel_Defaultweb.png)

Sau đó các bạn click chọn vào tên miền mà các bạn muốn dùng địa chỉ IP để truy cập trang web.

![](/img/CP_aaPanel_Defaultweb_Select.png)

![](/img/CP_aaPanel_Defaultweb_Check.png)

## 2. Cài đặt SSL cho trang web

Để cài đặt SSL cho tên miền, các bạn vào phần "**Website**" và click vào tên miền của các bạn tại ô **Site name**.

![](/img/CP_aaPanel_SSL.png)

Nó sẽ hiện bảng "**Site modification**", các bạn tìm tới phần ``SSL``.

Chọn ô "**Let's Encrypt**" để tạo một SSL miễn phí cho trang web các bạn.

![](/img/CP_aaPanel_SSL_Create.png)

![](/img/CP_aaPanel_SSL_process.png)

Sau khi chương trình chạy xong thì nó sẽ tự tạo chứng chỉ và private key cho bạn. Bạn ấn ô "Save" để lưu vào website của bạn.

![](/img/CP_aaPanel_SSL_Done.png)

# END