# Direct Admin

# Mục lục

- [Direct Admin](#direct-admin)
- [Mục lục](#mục-lục)
- [I. Direct Admin là gì](#i-direct-admin-là-gì)
  - [1. Khái niệm.](#1-khái-niệm)
  - [2. So sánh giữa Direct Admin và cPanel.](#2-so-sánh-giữa-direct-admin-và-cpanel)
- [II. Giao diện của Direct Admin](#ii-giao-diện-của-direct-admin)
- [III. Cài đặt website trên Direct Admin](#iii-cài-đặt-website-trên-direct-admin)
  - [1. Cài đặt thủ công](#1-cài-đặt-thủ-công)
  - [2. Cài đặt thông qua ternimal](#2-cài-đặt-thông-qua-ternimal)
  - [3. Cài đặt Wordpress bằng Direct Admin](#3-cài-đặt-wordpress-bằng-direct-admin)
- [ENd](#end)

# I. Direct Admin là gì

##  1. Khái niệm.

Cũng giống như cPanel thì Direct Admin cũng là một bảng điều khiển lưu trữ web dựa trên giao diện đồ họa web, cho phép quản lý các trang web thông qua trình duyệt web. Phần mềm này có thể được cấu hình để cho phép lưu trữ độc lập, lưu trữ đại lý (reseller) và lưu trữ chia sẻ từ một phiên bản duy nhất. DirectAdmin cũng cho phép quản lý các tác vụ của máy chủ và nâng cấp phần mềm gói (như Apache HTTP Server, PHP và MySQL) trực tiếp từ bảng điều khiển, giúp đơn giản hóa việc cấu hình máy chủ và lưu trữ.

## 2. So sánh giữa Direct Admin và cPanel.

Mặc dù giữa Direct Admin và cPanel đều có điểm chung là một bảng điều khiển để quản lí các dịch vụ web nhưng chúng đều có sự khác biệt nhất định.

* **Giao diện người dùng**

  **cPanel**: có giao diện trực quan hơn, với nhiều biểu tượng và tính năng hiển thị ngay từ màn hình chính. Mặc dù điều này giúp người dùng dễ dàng truy cập các chức năng, nhưng có thể khiến những người mới bắt đầu cảm thấy choáng ngợp. Ngoài ra, cPanel cung cấp khả năng tùy chỉnh giao diện thông qua các skin và sắp xếp các tính năng theo ý muốn.

  ![](/thuctap/img/DA_cPanelUI.png)

  **DirectAdmin**, ngược lại, có giao diện đơn giản và nhẹ nhàng hơn. Các tính năng được phân loại theo các tab và mục rõ ràng, giúp người dùng dễ dàng tìm thấy các công cụ cần thiết mà không cảm thấy quá tải. DirectAdmin không cung cấp nhiều tùy chọn tùy chỉnh giao diện như cPanel, nhưng giao diện gọn gàng và tối ưu hóa của nó làm cho việc sử dụng dễ dàng hơn đối với những người quản trị server có ít kinh nghiệm.

  ![](/thuctap/img/DA_UI.png)

* **Tài nguyên hệ thống**

  Dù cả hai có điểm chung là đều dựa trên hệ điều hành linux mà xây dụng lên nhưng vẫn có một số yêu cầu về tài nguyên hệ thống khác biệt.

  **cPanel**: Yêu cầu nhiều tài nguyên hơn do nhiều tính năng và giao diện đồ họa phong phú. Cần tối thiểu 1 GB RAM, nhưng 2 GB là khuyến nghị để chạy mượt mà.

  **DirectAdmin**: Nhẹ hơn và ít yêu cầu tài nguyên hơn. Có thể hoạt động hiệu quả với chỉ 512 MB RAM trong một số trường hợp.

* **Giá cả** 

  **cPanel**: Mấy năm gần đây đã có một số thay đổi về giá cả. Kể từ khi cPanel chuyển sang mô hình cấp phép theo tài khoản, mức giá đã tăng lên đáng kể, đặc biệt là đối với những nhà cung cấp dịch vụ hosting nhỏ hoặc trung bình.

  ![](/thuctap/img/cPanel_Price.png)

  **Direct Admin**: Sử dụng mô hình cấp phép đơn giản hơn, không tính phí theo số lượng tài khoản như cPanel. Thay vào đó, nó có các mức giá cố định cho từng loại giấy phép, giúp người dùng dễ dàng dự đoán chi phí.

  ![](/thuctap/img/DA_Price.png)

# II. Giao diện của Direct Admin

Giao diện của Direct Admin quả thực rất đơn giản và thân thiện, đặc biệt là đối với những người mới bắt đầu. Với thiết kế rõ ràng và dễ điều hướng, người dùng có thể dễ dàng tìm thấy các tính năng cần thiết mà không bị rối mắt. Một số điều lưu ý các bạn cần phải biết về giao diện của Direct Admin.

* **Thanh công cụ**

  Thanh công cụ trong DirectAdmin cung cấp nhiều chức năng quản lý server và hosting dành cho người quản trị web. Nó bao gồm các công cụ như quản lý tài khoản người dùng, quản lý email, tên miền, cơ sở dữ liệu, FTP, và nhiều tính năng khác.

  ![](/thuctap/img/DA_ToolBar.png)

* **Bảng điều khiển**

  Tại đây sẽ hiển thị thông tin tài nguyên mà bạn có trên tài khoản hosting.

  ![](/thuctap/img/DA_Dashboard.png)

# III. Cài đặt website trên Direct Admin

Tương tự như cPanel, Direct Admin cũng có nhiều cách để cài đặt trang web của bạn lên hosting

## 1. Cài đặt thủ công

Các bạn vào phần "**System Info & Files**" và click vào chữ "**File Manager**" để chuyển tới trang quản lí tệp tin của Direct Admin

![](/thuctap/img/DA_FileManager.png)

Sau khi các bạn đã vaò trang quản lí tệp tin, tiếp theo các bạn click vào thư mục "**public_html**" để vào trong đó upload mã nguồn các bạn lên hosting.

![](/thuctap/img/DA_Public_html.png)

![](/thuctap/img/DA_Upload_File.png)

Các bạn vào tên miền của các bạn để kiểm tra website đã được upload thành công chưa.

![](/thuctap/img/DA_CheckWebsite.png)

## 2. Cài đặt thông qua ternimal

Cách này yêu cầu người sử dụng hiểu được cách sử dụng cơ bản của ternimal, trình quản lí gói, cách phân quyền,...

Để vào được ternimal trong Direct Admin các bạn vào phần "**System Info & Files**" và click vào chữ "**Ternimal**" để vào mở ternimal của Direct Admin lên.

![](/thuctap/img/DA_Ternimal.png)

![](/thuctap/img/DA_Ternimal_Active.png)

Các bạn sử dụng các câu lệnh để tiến hành thao tác trong ternimal.

## 3. Cài đặt Wordpress bằng Direct Admin

Ngoài cách cài đặt wordpress bằng cách upload file lên bằng File Manager và tự tạo database. Thì còn một cách tự động khác là sử dụng **Wordpress Manager**

Để cài đặt, các bạn vào phần "**Advanced Features**" và click vào chữ "**Wordpress Manager**" để vào trang cài đặt Wordpress tự động.

![](/thuctap/img/DA_Wordpress.png)

Khi các bạn đã vào được trang cài đặt wordpress thì hãy ấn nút "Install" để tiến hành cài đặt.

![](/thuctap/img/DA_Wordpress_Install.png)

![](/thuctap/img/DA_Wordpress_Create.png)

Trong mục **Advanced mode** thì sẽ cho phép các bạn tự đặt mật khẩu, tên cho tài khoản admin và email của admin. Còn nếu các bạn không muốn hoặc không quan tâm thì lúc các click vào ô "**CREATE**" thì hệ thống sẽ tự động đặt mật khẩu ngẫu nhiên và dùng email admin của các bạn làm tài khoản đăng nhập, nó cũng tiện thể tự động tạo luôn database cho các bạn.

**Lưu ý nhỏ:** Việc cài đặt này sẽ ghi đè lên các tệp hiện có trong thư mục **public_html** nên các bạn như sao lưu lại các tệp tin quan trọng.

![](/thuctap/img/DA_Infor.png)

![](/thuctap/img/DA_Wordpress_Login.png)

# ENd

