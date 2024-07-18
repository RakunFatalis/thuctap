# PRIVATE ADDRESS

# MỤC LỤC


## 1. Private IP là gì?

Private IP là các địa chỉ hoạt động trong mạng cục bộ (local network). Các địa chỉ này không thể định tuyến trên Internet công cộng. Private IP được gán bởi bộ định tuyến (router) của mạng cho từng thiết bị cụ thể. Mỗi thiết bị trong cùng một mạng sẽ được cung cấp một địa chỉ IP riêng duy nhất. Điều này cho phép các thiết bị trong cùng một mạng giao tiếp với nhau mà không cần kết nối với Internet toàn cầu. Nhờ đó, các Private IP có thể cung cấp mức độ bảo mật cao hơn trong một mạng cụ thể. Private IP không thể được nhìn thấy trên Internet, khác với địa chỉ Public IP. Chỉ có các thiết bị trong mạng cục bộ mới có thể thấy địa chỉ của nhau.

**Các dải địa chỉ của địa chỉ IP riêng**

Địa chỉ IP riêng tồn tại trong các dải cụ thể được Cơ quan cấp số Internet (IANA) dành riêng. Các dải địa chỉ của địa chỉ IP riêng như sau:

* **Lớp A**: Dải địa chỉ từ 10.0.0.0 đến 10.255.255.255

* **Lớp B**: Dải địa chỉ từ 172.16.0.0 đến 172.31.255.255

* **Lớp C**: Dải địa chỉ từ 192.168.0.0 đến 192.168.255.255

Các dải địa chỉ ngoài những dải địa chỉ được gán cho Private IP sẽ được sử dụng để gán địa chỉ Public IP trên mạng, vì Public IP là duy nhất cho mỗi thiết bị trên Internet. Do đó, các mạng nội bộ có thể sử dụng các dải địa chỉ này để phân bổ địa chỉ IP riêng trong một mạng lưới cụ thể. Private IP có thể được tái sử dụng trên các mạng khác, điều này là không thể thực hiện được với Public IP.

![](/thuctap/img/ipprivate.png)
## 2. Mục đích sử dụng Private Ip

**Mạng gia đình**: Nhiều router trong gia đình sử dụng địa chỉ IP riêng để gán các địa chỉ duy nhất cho các thiết bị trong mạng gia đình. Điều này cho phép nhiều thiết bị như máy tính, điện thoại thông minh, TV và thiết bị IoT giao tiếp với nhau một cách an toàn.

**Mạng danh nghiệp**: Trong các tổ chức lớn, địa chỉ IP riêng được sử dụng để tạo các mạng lưới nội bộ kết nối các máy tính, máy chủ, máy in và các thiết bị khác. Điều này cho phép nhân viên chia sẻ tài nguyên và cộng tác trong khi vẫn đảm bảo sự bảo mật và riêng tư.

**Mạng Riêng Ảo (VPNs)**: VPNs tạo ra các kết nối được mã hóa qua các mạng công cộng, cho phép người dùng truy cập vào các mạng riêng từ xa.

**Điện Toán Đám Mây**: Nhiều nhà cung cấp dịch vụ đám mây cung cấp các đám mây riêng ảo (VPCs) làm nơi khách hàng có thể triển khai các tài nguyên như máy ảo, cơ sở dữ liệu và containers. Địa chỉ IP riêng được sử dụng trong VPCs để giúp các tài nguyên này giao tiếp với nhau trong khi vẫn tách biệt với môi trường của các khách hàng khác.


## 3. Lợi ích khi sử dụng Private IP

**Bảo mật**: Vì các địa chỉ Private IP không thể được truy cập từ bên ngoài, mạng nội bộ sẽ ít bị tấn công hơn. Điều này giúp bảo vệ dữ liệu và tài nguyên của tổ chức khỏi các mối đe dọa từ Internet.

**Khả năng mở rộng**: Các dải địa chỉ Private IP cung cấp không gian địa chỉ rộng rãi cho các lưới mạng từ nhỏ đến lớn, đáp ứng sự tăng trưởng của các thiết bị và dịch vụ trong tổ chức. Việc sử dụng các dải địa chỉ IP riêng như ``10.0.0.0/8``, ``172.16.0.0/12``, và ``192.168.0.0/16``, các tổ chức có thể mở rộng mạng của mình mà không lo ngại về việc thiếu địa chỉ IP.

**Tính linh hoạt**: Quản trị viên mạng có toàn quyền kiểm soát việc quản lý các địa chỉ IP riêng, cho phép phân bổ tài nguyên một cách hiệu quả và tùy chỉnh cấu hình mạng.

**Hiệu quả về chi phí**: Bằng cách sử dụng địa chỉ Private IP nội bộ, các tổ chức có thể tránh việc phải mua và quản lý các địa chỉ Public IP lớn, giảm chi phí liên quan đến kết nối Internet.

## 4. Những hạn chế của Private IP

**Khả năng truy cập hạn chế**: Do không thể truy cập trực tiếp từ Internet công cộng, các dịch vụ và thiết bị sử dụng Private IP cần phải thông qua NAT hoặc các phương pháp khác để truy cập từ xa. Điều này có thể gây khó khăn khi cần kết nối từ bên ngoài vào mạng nội bộ.

**Overhead của NAT**: NAT thường được sử dụng để chuyển đổi giữa địa chỉ Private IP và địa chỉ Public IP. Quá trình này yêu cầu xử lý và có thể làm tăng độ trễ và phức tạp hóa hệ thống, đặc biệt trong các mạng lưới lớn với nhiều thiết bị.

**Độ phức tạp trong quản lý**: Trong các mạng lưới lớn, việc quản lý địa chỉ Private IP có thể trở nên phức tạp do phải đảm bảo phân bổ hợp lý, cấu hình subnet đúng cách và quản lý định tuyến hiệu quả. Điều này đòi hỏi kiến thức và kỹ năng cao từ quản trị viên mạng.

**Vấn đề tương thích**: Khi cần tích hợp với các dịch vụ bên ngoài, đặc biệt là những dịch vụ yêu cầu địa chỉ Public IP, địa chỉ Private IP có thể gặp vấn đề về khả năng tương thích. Điều này có thể đòi hỏi các giải pháp phức tạp hơn để đảm bảo hoạt động mượt mà.
