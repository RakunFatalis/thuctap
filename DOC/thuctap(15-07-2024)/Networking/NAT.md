# NAT

# MỤC LỤC

- [NAT](#nat)
- [MỤC LỤC](#mục-lục)
  - [1. NAT là gì?](#1-nat-là-gì)
  - [2. Ưu và nhược điểm của NAT](#2-ưu-và-nhược-điểm-của-nat)
  - [3. Các loại NAT phổ biến](#3-các-loại-nat-phổ-biến)
  - [4. Các thuật ngữ liên quan đến NAT](#4-các-thuật-ngữ-liên-quan-đến-nat)
- [END](#end)




## 1. NAT là gì?

NAT (Network Address Translation) là một kỹ thuật cho phép chuyển đổi từ một địa chỉ IP này thành một địa chỉ IP khác. Thông thường NAT được sử dụng phổ biến trong mạng sử dụng địa chỉ cục bộ, cần truy cập đến mạng công cộng (Internet). Vị trí thực hiện NAT là Router biên kết nối giữa 2 mạng.

![](/img/nat.jpg)

NAT cũng có thể coi như một Firewall (tường lửa) cơ bản. NAT duy trì một bảng thông tin về mỗi gói tin được gửi qua. Khi một máy tính trên mạng kết nối đến 1 website trên Internet header của địa chỉ IP nguồn được thay thế bằng địa chỉ Public đã được cấu hình sẵn trên NAT sever, sau khi có gói tin trở về NAT dựa vào bảng record mà nó đã lưu về các gói tin, thay đổi địa chỉ IP đích thành địa chỉ của PC trong mạng và chuyển tiếp đi. Thông qua cơ chế đó quản trị mạng có khả năng lọc các gói tin được gửi đến hay gửi từ một địa chỉ IP và cho phép hay ngăn truy cập đến một port cụ thể.

## 2. Ưu và nhược điểm của NAT

**Ưu điểm của NAT**

* **Hiệu quả về chi phí**:
    
    Một trong những lợi ích lớn nhất của NAT là tiết kiệm chi phí. Đối với các doanh nghiệp nhỏ và vừa, NAT cung cấp một cách để kết nối nhiều thiết bị với Internet mà không cần phải mua nhiều địa chỉ IP. Bằng cách sử dụng NAT, các doanh nghiệp có thể bảo tồn tài nguyên và giảm chi phí kết nối Internet.

* **Cải thiện bảo mật**: 
    Một lợi ích khác của NAT là nó có thể giúp cải thiện bảo mật mạng. NAT ẩn các địa chỉ IP của các thiết bị trong mạng nội bộ đằng sau một địa chỉ công cộng duy nhất. Điều này làm cho hacker khó xác định và tấn công các thiết bị cá nhân trong mạng. Ngoài ra, NAT có thể được cấu hình để cho phép hoặc chặn các loại lưu lượng cụ thể, mang lại cho quản trị viên quyền kiểm soát lớn hơn đối với bảo mật mạng.

* **Bảo tồn địa chỉ IP**:

    Sử dụng NAT cho phép kết nối nhiều thiết bị với một kết nối Internet duy nhất, giúp bảo tồn địa chỉ IP công cộng, vốn là tài nguyên hạn chế. Bằng cách này, các tổ chức có thể giảm nhu cầu sử dụng địa chỉ IP công cộng và tránh phải mua thêm các địa chỉ này.

* **Tính linh hoạt**:

    NAT cung cấp tính linh hoạt trong thiết kế mạng bằng cách cho phép các mạng nội bộ sử dụng bất kỳ phạm vi địa chỉ IP nào. Điều này cho phép các tổ chức dễ dàng cấu hình lại mạng của họ mà không ảnh hưởng đến kết nối Internet. Ngoài ra, NAT cho phép các thiết bị trong mạng nội bộ giao tiếp với các thiết bị trên Internet bằng cách sử dụng các phạm vi địa chỉ IP khác nhau.

* **Quản lý mạng đơn giản**:

    NAT cũng mang lại lợi ích là làm cho việc quản lý mạng trở nên dễ dàng hơn. Các tổ chức có thể loại bỏ nhu cầu quản lý phức tạp các địa chỉ IP bằng cách sử dụng các địa chỉ IP riêng trên mạng nội bộ của họ. Một mạng có thể dễ dàng tiếp nhận các thiết bị mới mà không ảnh hưởng đến kết nối với Internet.

**Nhược điểm của NAT**

* **Tăng độ phức tạp của mạng lưới**: 

    NAT thêm một lớp phức tạp vào thiết kế mạng, làm cho việc xử lý sự cố và quản lý mạng trở nên khó khăn hơn. NAT có thể gây ra các vấn đề về tương thích với một số loại thiết bị mạng và phần mềm nhất định. Việc chuyển đổi Public IP thành Private IP và ngược lại là một công việc tốn kém. 
    
    Hơn nữa, NAT có thể gây ra các vấn đề về hiệu suất do tăng thêm tải cho mạng. Điều này đặc biệt là vấn đề đối với các mạng quy mô lớn có lưu lượng truy cập cao. Ngoài ra, NAT cũng có thể cản trở một số loại ứng dụng mạng, chẳng hạn như VoIP và hội nghị truyền hình, cần kết nối trực tiếp peer-to-peer.

* **Vấn đề về hiệu suất**:

    NAT có thể gây ra các vấn đề về hiệu suất. Việc xử lý thêm để dịch các địa chỉ IP có thể dẫn đến tốc độ mạng chậm hơn và độ trễ tăng lên. Ngoài ra, NAT giới hạn số lượng kết nối đồng thời tối đa mà một mạng có thể hỗ trợ.

* **Khó khăn với xác thực dựa trên IP**:

    NAT có thể làm cho việc xác thực dựa trên IP trở nên khó khăn hơn. Vì nhiều thiết bị trong mạng nội bộ chia sẻ cùng một địa chỉ IP công cộng, nên việc xác định các thiết bị cá nhân khi triển khai xác thực dựa trên IP có thể trở nên thách thức.


* **Thiếu kết nối trực tiếp (End-to-End Connectivity)**:

    NAT có thể ngăn cản kết nối trực tiếp giữa các thiết bị trên các mạng nội bộ khác nhau. Điều này có thể là vấn đề đối với một số ứng dụng, chẳng hạn như liên lạc thời gian thực, yêu cầu kết nối trực tiếp giữa các thiết bị. Độ trễ cũng tăng lên do việc xử lý không cần thiết trong việc chuyển đổi địa chỉ IP riêng thành địa chỉ IP công cộng và ngược lại.

## 3. Các loại NAT phổ biến

Hiện nay, NAT (Network Address Translation) được sử dụng rộng rãi với nhiều loại khác nhau, mỗi loại có cách thức hoạt động và ứng dụng riêng.

* **Static NAT (NAT tĩnh)**:

    **Cách thức hoạt động**: 
    
    Static NAT ánh xạ một địa chỉ IP riêng (private IP) với một địa chỉ IP công cộng (public IP) cụ thể. Điều này có nghĩa là mỗi khi một thiết bị nội bộ gửi dữ liệu ra ngoài, địa chỉ IP của nó sẽ được thay thế bằng địa chỉ IP công cộng được ánh xạ cố định.
    
    **Ứng dụng**: 
    
    Thường được sử dụng cho các máy chủ cần truy cập từ bên ngoài mạng, như máy chủ web hoặc máy chủ email, nơi cần một địa chỉ IP công cộng cố định.


* **Dynamic NAT (NAT động)**:

    **Cách thức hoạt động**: 
    
    Dynamic NAT ánh xạ một địa chỉ IP riêng với một địa chỉ IP công cộng được chọn từ một nhóm các địa chỉ IP công cộng có sẵn. Địa chỉ IP công cộng này có thể thay đổi mỗi khi thiết bị gửi dữ liệu ra ngoài.
    
    **Ứng dụng**: 
    
    Thường được sử dụng khi có một số lượng hạn chế địa chỉ IP công cộng và các thiết bị không yêu cầu một địa chỉ cố định.


* **PAT (Port Address Translation) hoặc NAT Overload**:

    **Cách thức hoạt động**: 
    
    PAT cho phép nhiều thiết bị trong mạng nội bộ chia sẻ một địa chỉ IP công cộng duy nhất bằng cách sử dụng các cổng (port). Mỗi khi một thiết bị gửi dữ liệu ra ngoài, PAT thay thế địa chỉ IP nội bộ và cổng của thiết bị đó bằng địa chỉ IP công cộng và cổng mới.
    
    **Ứng dụng**: 
    
    Thường được sử dụng trong các mạng gia đình và doanh nghiệp nhỏ, nơi mà nhiều thiết bị cần truy cập Internet mà chỉ có một địa chỉ IP công cộng.

## 4. Các thuật ngữ liên quan đến NAT

**Địa chỉ inside local**: Đây là địa chỉ IP được đặt cho 1 thiết bị ở mạng nội bộ bên trong. Nó không được cung cấp bởi NIC (Network Information Center).

**Địa chỉ inside global**: Đây là địa chỉ IP đã được đăng ký tại NIC. Địa chỉ inside global thường được dùng để thay thế cho địa chỉ IP inside local.

**Địa chỉ outside local**: Đây là địa chỉ IP của một thiết bị nằm ở mạng bên ngoài. Các thiết bị thuộc mạng bên trong sẽ tìm thấy thiết bị thuộc mạng bên ngoài thông qua địa chỉ IP này. Địa chỉ outside local không nhất thiết phải được đăng ký với NIC. Nó hoàn toàn có thể là một địa chỉ Private.

**Địa chỉ outside global**: Đây là địa chỉ IP được đặt cho một thiết bị nằm ở mạng bên ngoài. Địa chỉ này là một IP hợp lệ trên mạng internet.

# END