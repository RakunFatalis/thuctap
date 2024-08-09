# Cài đặt HAProxy

# Mục lục


Hệ thống được cài đặt với bộ cân bằng tải HAproxy và các webserver được cài trên các máy ảo CentOS 9. Địa chỉ IP các server:

HAProxy server: ``192.168.3.152``

Server 1: ``192.168.3.183``
Server 2: ``192.168.3.198``

Các Server 1 và Server 2 đã cài đặt webserver Nginx
# I. Cài đặt HAProxy

* **Bước 1: Cập nhật hệ thống**

    Trước tiên, hãy đảm bảo hệ thống của bạn đã được cập nhật:

    ``# yum update -y``

* **Bước 2: Cài đặt HAProxy**

    Sau khi cập nhật hệ thống, bạn có thể cài đặt HAProxy bằng lệnh:

    ``# yum install haproxy -y``

    ![](/img/install_HAProxy.png)

* **Bước 3: Kiểm tra phiên bản HAProxy**

    Để xác nhận rằng HAProxy đã được cài đặt thành công, bạn có thể kiểm tra phiên bản bằng cách chạy:

    ``# haproxy -v``

    ![](/img/HAProxy_ver.png)

# II. Cấu hình HAProxy

Trước khi chúng ta cấu hình HAProxy, chúng ta sẽ tìm hiểu file cấu hình chứa những thành phần gì. File cấu hình của HAProxy có tên ``haproxy.cfg``, thông thường nó sẽ nằm trong đường dẫn mặc định ``/etc/haproxy/haproxy.cfg``

Chúng ta sử dụng lệnh: ``# nano /etc/haproxy/haproxy.cfg`` để tìm hiểu trong file đó chứa những gì.

File ``haproxy.cfg`` thường có 4 phần chính **global**, **defaults**, **frontend** và **backend**. Các thành phần này sẽ định nghĩa cách máy chủ HAproxy tiếp nhận, xử lý yêu cầu, chọn máy chủ tiếp nhận yêu cầu và chuyển tiếp.

* **Global**

    Phần này cấu hình môi trường chung cho HAProxy. Nó quy định cách HAProxy ghi log, chạy với quyền nào, giới hạn kết nối và các cài đặt an ninh như sử dụng chroot. Đây là các cấu hình nền tảng giúp HAProxy hoạt động ổn định và bảo mật.

    ![](/img/HAProxy_Global.png)

* **Defaults**

    Các cấu hình trong phần này sẽ được áp dụng mặc định cho tất cả các frontend và backend trừ khi có cấu hình cụ thể khác. Ví dụ, nếu bạn có nhiều frontend hoặc backend, chúng sẽ kế thừa các thiết lập này trừ khi bạn ghi đè chúng trong phần tương ứng.

    ![](/img/HAProxy_Defaults.png)

* **Frontend**

    Phần frontend xác định cách xử lý các yêu cầu đến, bao gồm địa chỉ IP và cổng mà HAProxy lắng nghe. Nó cũng chỉ định backend mặc định mà các yêu cầu sẽ được chuyển tiếp. Đây là điểm vào đầu tiên cho lưu lượng mạng đi vào HAProxy.

    ![](/img/HAProxy_Frontend.png)

* **Backend**

    Phần backend xác định cách HAProxy chuyển tiếp các yêu cầu đến các máy chủ thực sự xử lý dữ liệu. HAProxy có thể sử dụng nhiều phương pháp để cân bằng tải giữa các máy chủ này, và kiểm tra sức khỏe của từng máy chủ để đảm bảo rằng chỉ các máy chủ khỏe mạnh mới nhận được yêu cầu.

    ![](/img/HAProxy_Backend.png)

Ngoài ra ta còn có:

* **Listen**

    Phần ``listen`` trong cấu hình HAProxy là một phần đặc biệt, kết hợp cả các chức năng của frontend và backend. Điều này có nghĩa là bạn có thể cấu hình một cổng hoặc IP để lắng nghe các kết nối đến và sau đó xử lý hoặc chuyển tiếp chúng đến các server đích, tất cả trong một khối cấu hình duy nhất.

* **Stats**

    Phần ``stats`` trong cấu hình HAProxy được sử dụng để bật và cấu hình giao diện thống kê của HAProxy. Giao diện này cung cấp một cái nhìn chi tiết về hoạt động của các frontend, backend, và server mà HAProxy đang quản lý.


Sau đây mình sẽ cấu hình **Frontend** với **Backend** HAProxy đơn giản, bạn có thể xem ảnh bên dưới để tham khảo:

![](/img/HAProxy_conf.png)


Sau khi các bạn đã cấu hình xong ta chạy lệnh: ``# systemctl restart haproxy`` để khởi động lại HAProxy cho nó áp dụng cấu hình đã thay đổi.

Ta mở trình duyệt web lên và nhập địa chỉ IP server của mình để mở trang giao diện thông kê. Theo như bài lab của mình thì địa chỉ IP của HAProxy là ``192.168.3.152`` 

Vì thế mình sẽ nhập trên giao diện web ``http://192.168.3.152/haproxy?stats``

![](/img/HAProxy_stats.png)

# END