# SUBNETTING, NETMASK AND CIDR

# MỤC LỤC


- [SUBNETTING, NETMASK AND CIDR](#subnetting-netmask-and-cidr)
- [MỤC LỤC](#mục-lục)
  - [I. SUBNETTING](#i-subnetting)
    - [1. Subnetting là gì?](#1-subnetting-là-gì)
    - [2. Tại sao lại cần subnetting.](#2-tại-sao-lại-cần-subnetting)
    - [3. Quy trình của Subnetting](#3-quy-trình-của-subnetting)
    - [4. Đặc điểm Subnetting](#4-đặc-điểm-subnetting)
  - [II. NETMASK](#ii-netmask)
    - [1. Netmask là gì?](#1-netmask-là-gì)
    - [2. Cách thức hoạt động của Subnet Masks](#2-cách-thức-hoạt-động-của-subnet-masks)
    - [3. Cách tính và xác định các lớp IP](#3-cách-tính-và-xác-định-các-lớp-ip)
    - [4. Lí do cần Subnet Mask](#4-lí-do-cần-subnet-mask)
  - [III. CIDR](#iii-cidr)
    - [1. CIDR là cái gì?](#1-cidr-là-cái-gì)
    - [2. CIDR khác gì hình thức Classful Addresses](#2-cidr-khác-gì-hình-thức-classful-addresses)
    - [3. Những lợi ích mà CIDR đem lại](#3-những-lợi-ích-mà-cidr-đem-lại)
    - [4. CIDR hoạt động ra sao](#4-cidr-hoạt-động-ra-sao)
- [END](#end)



## I. SUBNETTING

### 1. Subnetting là gì?

Subnetting là quá trình phân chia một mạng lớn (một dải địa chỉ IP) thành các mạng con nhỏ hơn. Điều này không chỉ giúp tối ưu hóa việc sử dụng địa chỉ IP mà còn giúp cải thiện hiệu suất và bảo mật của mạng.

### 2. Tại sao lại cần subnetting.

Mỗi doanh nghiệp đều cần một cách thiết kế mạng hiệu quả để truyền dữ liệu trơn tru và không lỗi qua kênh mạng.

Để khắc phục vấn đề sử dụng quá nhiều ID mạng, khái niệm chia mạng con được áp dụng trong hệ thống. Để hiểu điều này, hãy xem một số lý do sử dụng chia mạng con:

1. **Mạng con (Sub-network)**:

   * **Phân phối địa chỉ IP hiệu quả**: Subnetting giúp phân chia một dải địa chỉ IP lớn thành nhiều subnet nhỏ hơn theo nhu cầu cụ thể của mạng. Điều này giúp tổ chức các thiết bị trong mạng một cách hợp lý và hiệu quả.
   
   * **Quản lý dễ dàng**: Việc chia mạng thành các subnet nhỏ hơn giúp việc quản lý và giám sát trở nên dễ dàng hơn. 

2. **Tăng cường bảo mật (Increased Security)**:

   * **Thiết lập đơn vị bảo mật**: Subnetting giúp dễ dàng thiết lập các khu vực bảo mật riêng biệt trong mạng. Mỗi subnet có thể có các chính sách bảo mật và quyền truy cập riêng, giúp bảo vệ dữ liệu khỏi các vi phạm.
   
   * **Cô lập sự cố**: Khi có sự cố xảy ra, subnetting giúp cô lập và giải quyết vấn đề trong một subnet cụ thể mà không ảnh hưởng đến toàn bộ mạng.

3. **Ngăn chặn lãng phí địa chỉ IP (Prevent wastage of IP addresses)**:

   * **Sử dụng hiệu quả tài nguyên**: Bằng cách chia nhỏ mạng thành các subnet, subnetting giúp sử dụng địa chỉ IP một cách hiệu quả hơn, tránh lãng phí tài nguyên địa chỉ IP có sẵn.

4. **Giao tiếp tốt hơn giữa các mạng con (Better communication between subnets)**:
   
   * **Tối ưu hóa giao tiếp**: Subnetting giúp tối ưu hóa giao tiếp giữa các subnet, đảm bảo rằng dữ liệu được truyền một cách hiệu quả và nhanh chóng.
   
   * **Cải thiện hiệu suất mạng**: Việc chia mạng thành các subnet nhỏ hơn giúp giảm thiểu tắc nghẽn và cải thiện hiệu suất tổng thể của mạng.

### 3. Quy trình của Subnetting

Quá trình subnetting bao gồm việc chia nhỏ một địa chỉ IP thành các đơn vị nhỏ hơn có thể được gán cho các đơn vị mạng riêng lẻ trong mạng gốc. Điều này được thực hiện bằng cách sử dụng các kỹ thuật khác nhau.

Subnetting chia địa chỉ IP thành hai phần, đó là địa chỉ mạng và địa chỉ host.

Sau đó, sử dụng kỹ thuật subnet mask, bạn có thể tiếp tục chia nhỏ địa chỉ đã chia thành các đơn vị và gán chúng cho các thiết bị khác nhau trong mạng.

### 4. Đặc điểm Subnetting

Để thiết kế một mạng con (subnetwork), cần phải hiểu rõ một số đặc điểm sau:

* **IP Addresses (Số lượng địa chỉ IP)**: Đặc điểm này đại diện cho tổng số địa chỉ IP trong mạng con.

* **Network ID (ID mạng)**: Đây là địa chỉ IP đầu tiên trong mỗi mạng con trong ID mạng chính.

* **Broadcast ID (ID phát sóng)**: Đặc điểm này đại diện cho địa chỉ IP cuối cùng trong mỗi mạng con trong ID mạng.

* **First Host ID (ID máy chủ đầu tiên)**: Địa chỉ IP tiếp theo sau ID mạng được đại diện bởi ID máy chủ đầu tiên.

* **Last Host ID (ID máy chủ cuối cùng)**: Địa chỉ IP ngay trước ID phát sóng được đại diện là ID máy chủ cuối cùng.

* **Next Network (Mạng kế tiếp)**: Đặc điểm này gán ID mạng cho mạng con kế tiếp.

Bạn xem ảnh dưới để hiểu rõ hơn

![](/img/subnetting.png)


## II. NETMASK

### 1. Netmask là gì?

Netmask (hay còn gọi là subnet mask) là một con số được sử dụng để xác định phần mạng và phần host của một địa chỉ IP trong mạng máy tính. Netmask định nghĩa rõ ràng các bit trong địa chỉ IP mà thuộc về phần mạng và phần host. Về cơ bản, nó là một dãy số nhị phân, có thể được biểu diễn dưới dạng dấu chấm (ví dụ: 255.255.255.0).

Netmask quyết định số lượng địa chỉ IP có thể được sử dụng trong mỗi mạng con và cách phân chia các mạng con trong mạng lớn hơn. Nó là một phần quan trọng của việc cấu hình mạng và routing trong hệ thống mạng.

### 2. Cách thức hoạt động của Subnet Masks

Subnetting (chia mạng con) là kỹ thuật chia một mạng lớn thành nhiều mạng con nhỏ hơn (subnet). Mỗi subnet có dải địa chỉ IP riêng và hoạt động như một mạng độc lập, giúp giảm lưu lượng mạng, tăng tính bảo mật và linh hoạt trong quản lý mạng.

Cách thức nó hoạt động như sau:

1. **Xác định mạng và host**: Subnet Mask dùng để phân biệt phần mạng và phần host trong địa chỉ IP. Nó chỉ ra rõ các bit trong địa chỉ IP mà thuộc về mạng (network portion) và các bit mà thuộc về host (host portion).

2. **Biểu diễn bằng dãy số nhị phân**: Subnet Mask được biểu diễn dưới dạng một dãy số nhị phân có độ dài cố định, thường là 32 bit cho IPv4 và 128 bit cho IPv6. Các bit 1 trong Subnet Mask đại diện cho phần mạng, và các bit 0 đại diện cho phần host.

3. **Áp dụng trong quá trình routing và định tuyến**: Khi một gói tin IP được gửi đi, hệ thống mạng sẽ sử dụng Subnet Mask để xác định xem địa chỉ IP của đích đến thuộc cùng một mạng con với thiết bị gửi hay không. Điều này giúp hệ thống quyết định liệu gói tin cần được gửi trực tiếp tới đích hay thông qua một bộ định tuyến (router).

4. **Phân chia mạng con**: Bằng cách sử dụng Subnet Mask, một mạng lớn có thể được chia thành nhiều mạng con nhỏ hơn, mỗi mạng con có thể có số lượng địa chỉ IP khác nhau, phụ thuộc vào độ dài của Subnet Mask được áp dụng.

### 3. Cách tính và xác định các lớp IP

Có năm lớp chính được xác định trong hệ thống địa chỉ IP phiên bản 4 (IPv4) - lớp A, B, C, D, và E. Mỗi lớp có đặc điểm và phạm vi địa chỉ riêng biệt, phù hợp với các mục đích sử dụng khác nhau. Dưới đây là hướng dẫn về cách tính và xác định lớp của một địa chỉ IP dựa trên những bit đầu tiên của nó.

* **Lớp A**: Nếu bit đầu tiên của địa chỉ IP là 0, địa chỉ đó thuộc lớp A. Phạm vi của lớp A là từ 0.0.0.0 đến 127.255.255.255. Điều này cho phép mạng lớp A hỗ trợ một số lượng lớn các hosts.

* **Lớp B**: Nếu hai bit đầu tiên là 10, địa chỉ đó thuộc lớp B. Phạm vi của lớp B là từ 128.0.0.0 đến 191.255.255.255, hỗ trợ một số lượng vừa phải các mạng và hosts.

* **Lớp C**: Địa chỉ IP thuộc lớp C nếu ba bit đầu tiên là 110. Phạm vi của lớp C là từ 192.0.0.0 đến 223.255.255.255, chủ yếu dùng cho các mạng nhỏ với ít hosts hơn.

* **Lớp D**: với bốn bit đầu là 1110, phạm vi từ 224.0.0.0 đến 239.255.255.255, được dùng cho mục đích đa phương tiện và nhóm đa điểm (multicast).

* **Lớp E**: từ 240.0.0.0 đến 255.255.255.255, dành riêng cho mục đích thử nghiệm và nghiên cứu.

![](/img/classIP.png)

### 4. Lí do cần Subnet Mask

Subnet mask là một phần quan trọng của địa chỉ IP vì nó giúp xác định phạm vi mạng và host trong một mạng con. Đây là những lí do chính tại sao cần sử dụng subnet mask:

1. **Phân biệt mạng và host**: Subnet mask xác định phần mạng và phần host của địa chỉ IP. Nó cho phép các thiết bị mạng biết được đâu là địa chỉ mạng và đâu là địa chỉ host trong một mạng con cụ thể.

2. **Phân vùng mạng**: Giúp chia nhỏ một mạng lớn thành các mạng con nhỏ hơn, điều này giúp tối ưu hóa quản lý và sử dụng địa chỉ IP.

3. **Định tuyến (Routing)**: Các thiết bị mạng sử dụng subnet mask để xác định xem liệu một địa chỉ IP có nằm trong cùng một mạng hay khác mạng để quyết định định tuyến dữ liệu.

4. **Bảo mật**: Subnet mask cũng có thể được sử dụng để áp dụng các quy tắc bảo mật theo phạm vi mạng hoặc host, cho phép kiểm soát truy cập vào mạng hoặc từ mạng.

5. **Quản lý tài nguyên mạng**: Bằng cách phân chia mạng thành các mạng con, bạn có thể dễ dàng quản lý và phân phối tài nguyên mạng như băng thông, địa chỉ IP, v.v.

Qua những lý do trên, việc tính toán và chia Subnet Mask không chỉ giúp tối ưu hóa việc sử dụng địa chỉ IP mà còn tăng cường an ninh, hiệu suất và sự linh hoạt trong quản lý mạng. Đây là những yếu tố quan trọng để duy trì hệ thống mạng hiệu quả và an toàn.

## III. CIDR

### 1. CIDR là cái gì?

**CIDR** là viết tắt của "Classless Inter-Domain Routing" (Định tuyến liên miền không lớp), là một phương pháp phân bổ địa chỉ IP để cải thiện hiệu quả định tuyến dữ liệu trên Internet. Mỗi thiết bị, máy chủ và thiết bị người dùng kết nối với Internet đều có một số duy nhất gọi là địa chỉ IP. Các thiết bị sử dụng địa chỉ IP này để tìm và giao tiếp với nhau.

Trước khi CIDR được sử dụng, Internet sử dụng mô hình phân lớp (Classful Networking) để quản lý địa chỉ IP. Tuy nhiên, mô hình này không linh hoạt và dẫn đến lãng phí địa chỉ IP. CIDR giải quyết vấn đề này bằng cách cho phép phân chia mạng một cách linh hoạt hơn, không bị ràng buộc vào các lớp cụ thể.

Mỗi địa chỉ CIDR bao gồm một địa chỉ IP và một số (thường được biểu thị bằng "prefix length") cho biết số lượng bit trong phần mạng của địa chỉ đó. Ví dụ, địa chỉ CIDR có thể là 192.168.1.0/24, trong đó "/24" cho biết rằng 24 bit đầu của địa chỉ IP này là phần mạng, còn lại là phần máy chủ.

Qua đó, CIDR giúp tối ưu hóa việc phân bổ địa chỉ IP và quản lý mạng hiệu quả hơn trên Internet, đồng thời cải thiện khả năng định tuyến dữ liệu.

### 2. CIDR khác gì hình thức Classful Addresses

Trước khi CIDR được sử dụng, hệ thống phân lớp IPv4 chia địa chỉ IP thành ba lớp chính: A, B và C. Mỗi lớp có độ dài và phân bổ bit khác nhau cho phần mạng và phần máy chủ của địa chỉ IP.

* **Lớp A**: Một địa chỉ IPv4 Lớp A có 8 bit tiền tố mạng. Ví dụ: 44.0.0.1, trong đó 44 là địa chỉ mạng và 0.0.1 là địa chỉ máy chủ.

* **Lớp B**: Một địa chỉ IPv4 Lớp B có 16 bit tiền tố mạng. Ví dụ: 128.16.0.2, trong đó 128.16 là địa chỉ mạng và 0.2 là địa chỉ máy chủ.

* **Lớp C**: Một địa chỉ IPv4 Lớp C có 24 bit tiền tố mạng. Ví dụ: 192.168.1.100, trong đó 192.168.1 là địa chỉ mạng và 100 là địa chỉ máy chủ.

Mô hình phân lớp này cung cấp các lớp có kích thước cố định và phân bổ địa chỉ không linh hoạt.

CIDR là phương pháp sử dụng "variable length subnet masking" (VLSM) để linh hoạt hóa số lượng bit cho phần mạng và phần máy chủ trong địa chỉ IP. Thay vì phân bổ địa chỉ theo các lớp cụ thể, CIDR cho phép định tuyến mạng một cách hiệu quả hơn bằng cách chỉ định số lượng bit tiền tố mạng.

**Ví dụ**:
* Địa chỉ CIDR IPv4 192.0.2.0/24, trong đó "/24" chỉ ra rằng 24 bit đầu của địa chỉ này (192.0.2) là phần network, còn lại là phần host. Điều này cho phép mạng được phân chia thành các mạng con có kích thước khác nhau, tối ưu hóa việc sử dụng địa chỉ IP và quản lý mạng.

CIDR đã thay thế mô hình phân lớp trước đây bằng cách cung cấp sự linh hoạt hơn trong việc sử dụng và quản lý địa chỉ IP, làm tăng hiệu suất và hiệu quả của hệ thống định tuyến trên Internet.

### 3. Những lợi ích mà CIDR đem lại

CIDR mang lại nhiều lợi ích cho tổ chức trong việc phân bổ địa chỉ IP và định tuyến dữ liệu giữa các thiết bị:

* **Giảm lãng phí địa chỉ IP**:
   
   CIDR cung cấp linh hoạt khi xác định phân vùng mạng và máy chủ trên địa chỉ IP. Tổ chức có thể sử dụng CIDR để cấp phát số lượng địa chỉ IP cần thiết cho một mạng cụ thể và giảm thiểu lãng phí. Thay vì bị ràng buộc vào các lớp cố định, CIDR cho phép phân chia mạng thành các mạng con có kích thước linh hoạt hơn, tối ưu hóa việc sử dụng địa chỉ IP.

* **Định tuyến dữ liệu nhanh chóng**:
   
   CIDR cho phép các bộ định tuyến tổ chức các địa chỉ IP thành nhiều mạng con một cách hiệu quả hơn. Mạng con là một mạng nhỏ tồn tại trong một mạng lớn. Với CIDR, tổ chức có thể tạo và tổng hợp các mạng con, giúp dữ liệu đến được địa chỉ đích mà không đi qua các đường dẫn không cần thiết.

* **Tạo một Máy chủ ảo riêng (VPC)**:
   
   Máy chủ ảo riêng là không gian kỹ thuật số riêng được lưu trữ trong đám mây, cho phép tổ chức cấp phát công việc trong môi trường được cô lập và an toàn. VPC sử dụng địa chỉ IP CIDR khi truyền dữ liệu giữa các thiết bị kết nối.

* **Tạo các siêu mạng một cách linh hoạt**:
   
   Siêu mạng là một nhóm các subnet có các tiền tố mạng tương tự. CIDR cho phép linh hoạt trong việc tạo các siêu mạng, điều này không thể có trong kiến trúc mặt nạ truyền thống. Ví dụ, tổ chức có thể kết hợp các địa chỉ IP thành một khối mạng duy nhất bằng cách sử dụng một ghi chú như sau:

   192.168.1.0/23
   192.168.0.0/23

   Ghi chú này áp dụng subnet mask là 255.255.254.0 cho địa chỉ IP, trả về 23 bit đầu tiên là địa chỉ mạng. Bộ định tuyến chỉ cần một mục bảng định tuyến để quản lý các gói dữ liệu giữa các thiết bị trên các subnet.

Tóm lại, CIDR mang lại sự linh hoạt và hiệu quả trong phân bổ và quản lý địa chỉ IP, cũng như trong định tuyến dữ liệu trên mạng, giúp tối ưu hóa sử dụng nguồn lực mạng và hỗ trợ mở rộng các mạng một cách hiệu quả trên Internet.

### 4. CIDR hoạt động ra sao

CIDR cho phép các bộ định tuyến mạng định tuyến các gói dữ liệu đến thiết bị tương ứng dựa trên mạng con được chỉ định. Thay vì phân loại địa chỉ IP dựa trên các lớp cụ thể, CIDR lấy thông tin về địa chỉ mạng và máy chủ như đã chỉ định bởi hậu tố CIDR.

Để hiểu cách CIDR hoạt động, quan trọng phải hiểu về khái niệm các CIDR blocks và CIDR notation.

**CIDR blocks**

Một CIDR blocks là một tập hợp các địa chỉ IP chia sẻ cùng tiền tố mạng và số bit. Một khối lớn bao gồm nhiều địa chỉ IP hơn và có hậu tố nhỏ hơn.

Internet Assigned Numbers Authority (IANA) giao các CIDR blocks lớn cho các cơ quan đăng ký internet khu vực (RIR). Sau đó, RIR phân phối các khối nhỏ hơn cho các cơ quan đăng ký internet địa phương (LIR), sau đó chuyển giao cho các tổ chức. Đồng thời, người dùng cá nhân có thể xin các kCIDR blocks từ nhà cung cấp dịch vụ internet của họ.

![](/img/CIDRblock.png)


**CIDR notation**

**Ghi chú CIDR** biểu diễn một địa chỉ IP và một hậu tố chỉ ra số bit xác định mạng trong một định dạng cụ thể. Ví dụ, bạn có thể biểu diễn địa chỉ 192.168.1.0 với một hậu tố 22-bit mạng như là 192.168.1.0/22.

CIDR cho phép mạng tổ chức các địa chỉ IP một cách hiệu quả hơn, cải thiện khả năng quản lý và định tuyến dữ liệu trên Internet bằng cách sử dụng các mạng con có kích thước biến đổi linh hoạt. Điều này giúp tối ưu hóa việc sử dụng không gian địa chỉ IP và hỗ trợ mở rộng mạng lưới internet một cách hiệu quả.


# END