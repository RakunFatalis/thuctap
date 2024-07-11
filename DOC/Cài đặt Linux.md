# Cài đặt Linux
  * Có rất nhiều bản distro phổ biến của Linux trên thế giới như là CentOs, Debian, Ubuntu,...
    
    Tại bài hướng dẫn này mình sẽ cài bản distro Linux Ubuntu Minimal
# MỤC LỤC
[Yêu cầu cấu hình](#Y)

[1. Chuẩn bị và cài đặt](#1)
- [Tải ISO và tạo USB boottable](#1.1)
- [Cấu hình BIOS/UEFI để khởi động từ USB](#1.2)

[2. Quá trình cài đặt](#2)

[END](#E)
<a name="Y"></a>
## Yêu cầu cấu hình
* Để cài hệ điều hành Ubuntu cần thỏa những yêu cầu sau:

  - Chip hai nhân 2 GHz, 4GB RAM.

  - Đảm bảo máy tính bạn cần phải trống ít nhất 25 GB ổ cứng.

  - Laptop, PC cần phải có cổng USB trống.
<a name="1"></a>
## 1. Chuẩn bị cài đặt
<a name="1.1"></a>
### Tải ISO và tạo USB bootable

***Bước 1: Tải file ISO của Ubuntu***

* **Ta vào trang web của [Ubuntu](https://ubuntu.com/download/desktop#release-notes)**

![Image description](/img/web%20ubuntu.png)

* **Ta click vào ô màu xanh để file ISO về**

![Image description](/img/web%20ubuntu%20select.png)

***Bước 2: Ta tải USB Bootloader Rufus***

* **Ta vào trang web của [Rufus](https://rufus.ie/en/)**

![Image description](/img/web%20Rusfu.png)

* **Kéo xuống dưới và ta thấy một bảng các phiên bản Rufus**

![Image description](/img/Rufusdown.png)

* **Ta chọn phiên bản *rufus-4.5.exe***

![Image description](/img/Rufusdownselect.png)

***Bước 3: Tạo USB Boot***
  1. Chọn USB mà bạn muốn tạo
  2. Chọn file ISO cài đặt
  3. Tạo USB boot 

![Image description](/img/StepRufus.png)

<a name="1.2"></a>
### Cấu hình BIOS/UEFI để khởi động từ USB
***Bước 1: Truy cập vào BIOS của máy tính. Tuỳ từng hãng sẽ có cách vào bios khác nhau.***

| Hãng          | Cách vào BIOS               |
| --------------| --------------------------- |
| Acer          | F12 hoặc Esc, F9            |
| Asus          | F8 hoặc Esc                 |
| Dell          | F12                         |
| HP            | ESC hoặc F9                 |
| Lenovo        | F12, F8, F10 hoặc Fn + F11  |


***Bước 2: Sau khi mở được BIOS đầu tiên chúng ta sẽ thấy giao diện này. Giao diện này có thể sẽ có màu sắc và bố cục hơi khác nhau trên từng dòng máy tính, nhưng các tính năng vẫn sẽ tương tự.***

![Image description](/img/biosmenu.png)

**Dùng các phím mũi tên hoặc chuột để di chuyển đến tab Boot Menu(có thể ấn hotkey F8 để vào).**

![Image description](/img/bootmenuselect.png)

***Bước 3: Chọn USB flash drive/CD-ROM trong Boot Menu mà bạn muốn sử dụng***

![Image description](/img/USBdrive.png)

***Bước 4: Vẫn trong BIOS, ta ấn hotkey F7 hoặc click chuột để vào [Advanced Mode]***

![Image description](/img/F7.png)

* Trong phần màn hình **Boot**, ta chọn mục **[Fast Boot]** rồi chọn **Disabled**

![Image description](/img/bootstep.png)

* Vào mục **Security**, sau đó chọn **Secure Boot**

![Image description](/img/Security.png)

* Sau khi vào màn hình **Secure Boot**, chọn mục **Secure Boot Control** rồi chọn **Disabled**

![Image description](/img/SecureBoostDis.png)

* Ta nhấn **F10** để lưu lại và thoát, sau đó máy tính sẽ tự động khởi động lại

![Image description](/img/Save&Exit.png)

* **Lặp lại Bước 1, 2 và 3 để boot Ubuntu**
<a name="2"></a>
## 2. Quá trình cài đặt

### Dùng phím mũi tên để di chuyển và nhấn Enter để chọn

![Image description](/img/UbuntuGNU.png)

### Chọn ngôn ngữ cho Ubuntu

![Image description](/img/SelectLang.png)

### Chọn layout bàn phím

![Image description](/img/LayoutKey.png)

### Chọn bản khởi tạo

![Image description](/img/Typeinstall.png)

### Cấu hình IP cho máy

![Image description](/img/IPConfig.png)

### Cấu hình Proxy cho máy, nếu bạn không có proxy thì bỏ qua

![Image description](/img/ProxyConfig.png)

### Cấu hình mirror location

![Image description](/img/MirrorLocation.png)

### Cấu hình dung lượng cho máy

![Image description](/img/StorageCon.png)

* Tại đây có 2 lựa chon cho bạn
    1. **Use an entire disk** là lựa chọn sẽ cài đặt Ubuntu trên ổ cứng đã chọn.
    2. **Custom storage layout** là lựa chọn bạn sẽ tự cấu hình ổ cứng của máy.
    ![Image description](/img/StorageOpt.png)
    
    * ***Nếu bạn chon cách 2 thì hãy xem hướng dẫn sau đây***

        Đây là giao diện chính của Custom storage layout, bạn dùng phím mũi tên để di chuyển tới **free space** rồi nhấn **ENTER**
    
    ![Image description](/img/mainstoragescreen.png)

    * Tiếp đến chọn **Add GPT Partition**

    ![Image description](/img/GPTPa.png)
    * Phân vùng
      1. Các bạn phân vùng /boot: dung lượng 300MB
      2. Phân vùng /: tất cả dung lượng còn lại
    * Format: Các bạn chọn định dạng XFS hay EXT4 tuỳ vào mục đích sử dụng của các bạn. Thông thường ta sẽ chọn XFS vì nó hiệu suất tốt hơn so EXT4 vì EXT4 đã khá là cũ.
    Ta nhấn **ENTER** để tạo

    ![Image description](/img/MountFormat.png)
    
    Sau khi đã phân chia xong ta nhấn **DONE** để hoàn tất.

    ![Image description](/img/PaDone.png)

### Thiết lập thông tin tài khoản
* Đây là Profile setup của bạn:
    * Your Name: Tên của bạn
    * Your Server's Name: Tên máy chủ của bạn
    * Pick a username: Tên người dùng
    * Chosse a password: Đặt mật khẩu
    * Confirm your password: Nhập lại mật khẩu
    
    ![Image description](/img/Account.png)

### SSH setup
* Các bạn nhớ cài Install OpenSSH server. Nếu các bạn cài đặt máy chủ thực sự thì nó là điều kiện bắt buộc phải có để các bạn có thể truy cập vào máy chủ từ xa. Còn nếu không cần thì các bạn có thể bỏ qua bước này.
    
    ![Image description](/img/OpenSSH.png)

### Kiểm tra dịch vụ.

![Image description](/img/Featured.png)

### Hoàn tất
* **Tới đây các bạn chờ tải xong rồi reboot lại là hoàn tất quá trình cài đặt**
![Image description](/img/Done.png)

<a name="Y"></a>
# END