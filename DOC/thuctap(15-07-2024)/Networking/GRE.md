# Generic Routing Encapsulation

# Mục lục

- [Generic Routing Encapsulation](#generic-routing-encapsulation)
- [Mục lục](#mục-lục)
  - [1. GRE là gì?](#1-gre-là-gì)
  - [2. Tính năng](#2-tính-năng)
  - [3. GRE header](#3-gre-header)
  - [4. Phân loại GRE](#4-phân-loại-gre)
- [END](#end)


## 1. GRE là gì?

Generic routing encapsulation (GRE) là một giao thức sử dụng để thiết lập các kết nối point-to-point một các trực tiếp giữa các node trong mạng. Đây là một phương pháp đơn giản và hiệu quả để chuyển dữ liệu thông qua mạng public network, như Internet. GRE cho phép hai bên chia sẻ dữ liệu mà họ không thể chia sẻ với nhau thông qua mạng public network.

GRE đóng gói dữ liệu và chuyển trực tiếp tới thiết bị mà de-encapsulate gói tin và định tuyến chúng tới đích cuối cùng. Gói tin và định tuyến chúng tới đích cuối cùng. GRE cho pháp các switch nguồn và đích hoạt động như một kết nối ảo point-to-point với các thiết bị khác (bởi vì outer header được áp dụng với GRE thì trong suốt với payload được đóng gói bên trong).

## 2. Tính năng

GRE thêm vào tối thiểu 24 byte vào gói tin, trong đó bao gồm 20-byte IP header mới, 4 byte còn lại là GRE header. GRE có thể tùy chọn thêm vào 12 byte mở rộng để cung cấp tính năng tin cậy như: checksum, key chứng thực, sequence number.

![](/img/GRE.jpg)

GRE là công cụ tạo tunnel khá đơn giản nhưng hiệu quả. Nó có thể tạo tunnel cho bấy kì giao thức lớp 3 nào. GRE cho phép những giao thức định tuyến hoạt động trên kênh truyền của mình. GRE không có cơ chế bảo mật tốt.

Trong khi đó, IPSec cung cấp sự tin cậy cao. Do đó nhà quản trị thường kết hợp GRE với IPSec để tăng tính bảo mật, đồng thời cũng hỗ trợ IPSec trong việc định tuyến và truyền những gói tin có địa chỉ IP Muliticast.

## 3. GRE header

GRE header bản thân nó chứa đựng 4 byte, đây là kích cỡ nhỏ nhất của một GRE header khi không thêm vào các tùy chọn. 2 byte đầu tiên là các cờ (flags) để chỉ định những tùy chọn GRE. Những tùy chọn này nếu được active, nó thêm vào GRE header. Bảng sau mô tả những tùy chọn của GRE header.

![](/img/gre_table.jpg)

Trong GRE header 2 byte còn lại chỉ định cho trường giao thức. 16 bits này xác định kiểu của gói tin được mang theo trong GRE tunnel. Hình sau mô tả cách mà một gói tin GRE với tất cả tùy chọn được gán vào một IP header và data.

![](/img/gre_table_2.jpg)

## 4. Phân loại GRE

GRE là giao thức có thể đóng gói bất kì gói tin nào của lớp network. GRE cung cấp khả năng có thể định tuyến giữa những mạng riêng (private network) thông qua môi trường Internet bằng cách sử dụng các địa chỉ IP đã được định tuyến. GRE truyền thống là point-to-point, còn mGRE là sự mở rộng khái niệm này bằng việc cho phép một tunnel có thể đến được nhiều điểm đích, mGRE tunnel là thành phần cơ bản nhất trong DMVPN.

**Point-to-Point GRE**

Đối với các tunnel GRE point-to-point thì trên mỗi router spoke (R2 & R3) cấu hình một tunnel chỉ đến HUB (R1) ngược lại, trên router HUB cũng sẽ phải cấu hình hai tunnel, một đến R2 và một đến R3. Mỗi tunnel như vậy thì cần một địa chỉ IP. Giả sử mô hình trên được mở rộng thành nhiều spoke, thì trên R1 cần phải cấu hình phức tạp và tốn không gian địa chỉ IP.

![](/img/gre_PTP.jpg)


Trong tunnel GRE point-To-point, điểm đầu và cuối được xác định thì có thể truyền dữ liệu. Tuy nhiên, có một vấn đề phát sinh là nếu địa chỉ đích là một multicast (chẳng hạn 224.0.0.5) thì GRE point-to-point không thực hiện được. Để làm được việc này thì phải cần đến mGRE.


**Point-to-Multipoint GRE (mGRE)**

Như vậy, mGRE giải quyết được vấn đề đích đến là một địa chỉ multicast. Đây là tính năng chính của mGRE được dùng để thực thi Multicast VPN trong Cisco IOS. Tuy nhiên, trong mGRE, điểm cuối chưa được xác định nên nó cần một giao thức để ánh xạ địa chỉ tunnel sang địa chỉ cổng vật lý. Giao thức này được gọi là NHRP (Next Hop Resolution Protocol)

![](/img/gre_PTM.jpg)

# END