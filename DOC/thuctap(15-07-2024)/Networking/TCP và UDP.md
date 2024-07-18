# TCP AND UDP

# MỤC LỤC

- [TCP AND UDP](#tcp-and-udp)
- [MỤC LỤC](#mục-lục)
  - [I. Giao thức TCP](#i-giao-thức-tcp)
    - [1. Giao thức TCP là gì?](#1-giao-thức-tcp-là-gì)
    - [2. Cách hoạt động của TCP](#2-cách-hoạt-động-của-tcp)
    - [3. Quá trình thiết lập kết nối TCP (three-way handshake)](#3-quá-trình-thiết-lập-kết-nối-tcp-three-way-handshake)
    - [4. Quá trình chấm dứt kết nối TCP (TCP teardown)](#4-quá-trình-chấm-dứt-kết-nối-tcp-tcp-teardown)
    - [5. Cấu trúc header của TCP](#5-cấu-trúc-header-của-tcp)
  - [II. Giao thức UDP](#ii-giao-thức-udp)
    - [1. Giao thức UDP là gì ?](#1-giao-thức-udp-là-gì-)
    - [2. Các đặc tính của UDP](#2-các-đặc-tính-của-udp)
    - [3. Cấu trúc header của UDP](#3-cấu-trúc-header-của-udp)
- [END](#end)


## I. Giao thức TCP

### 1. Giao thức TCP là gì?

**Transmission Control Protocol** (TCP) là giao thức tiêu chuẩn trên Internet đảm bảo trao đổi thành công các gói dữ liệu giữa các thiết bị qua mạng. TCP là giao thức truyền tải cơ bản cho nhiều loại ứng dụng, bao gồm máy chủ web và trang web, ứng dụng email, FTP và các ứng dụng ngang hàng.

TCP hoạt động với giao thức Internet (IP) để chỉ định cách dữ liệu được trao đổi trực tuyến. IP chịu trách nhiệm gửi từng gói đến đích của nó, trong khi TCP **đảm bảo rằng các byte được truyền theo thứ tự mà chúng được gửi mà không có lỗi hoặc thiếu sót nào**. Hai giao thức kết hợp với nhau được gọi là TCP/IP.


### 2. Cách hoạt động của TCP

Giao thức TCP (Transmission Control Protocol) cho phép truyền thông tin hai chiều giữa các hệ thống máy tính. Điều này có nghĩa là các hệ thống này có thể gửi và nhận dữ liệu đồng thời, tương tự như một cuộc trò chuyện điện thoại. TCP sử dụng các đoạn (segments hay còn gọi là gói tin) là đơn vị cơ bản để truyền dữ liệu. Ngoài phần dữ liệu (payload), các đoạn còn chứa thông tin điều khiển và có giới hạn là 1.500 byte.

Phần mềm TCP trong ngăn xếp giao thức mạng của hệ điều hành có trách nhiệm thiết lập và chấm dứt các kết nối end-to-end cũng như truyền dữ liệu. Phần mềm này được điều khiển bởi các ứng dụng mạng như trình duyệt web hoặc máy chủ thông qua các giao diện cụ thể.

Mỗi kết nối TCP luôn phải được xác định bởi hai đầu điểm rõ ràng (client và server). Không quan trọng là bên nào đảm nhận vai trò client và bên nào đảm nhận vai trò server. Quan trọng là phần mềm TCP được cung cấp với một cặp định danh duy nhất và có thứ tự gồm địa chỉ IP và cổng (port), còn được gọi là "2-tuple" hay "socket" cho mỗi đầu điểm.

### 3. Quá trình thiết lập kết nối TCP (three-way handshake)  

Quá trình thiết lập kết nối TCP là quá trình bắt buộc và cơ bản để hai thiết bị thiết lập kết nối và bắt đầu truyền dữ liệu.

Dưới đây là giải thích chi tiết về quá trình này:

* **Bước 1: Client gửi SYN (Synchronize)**:

    * Quá trình bắt đầu khi client muốn thiết lập kết nối với server. Client gửi một gói tin SYN đến server.

    * Gói tin SYN chứa một số ngẫu nhiên (sequence number) để đảm bảo việc truyền dữ liệu không bị trùng lặp và đến đúng thứ tự.

* **Bước 2: Server gửi SYN-ACK (Synchronize-Acknowledgment)**:

    * Nếu server nhận được gói tin SYN từ client, nó sẽ gửi lại một gói tin SYN-ACK cho client.
    
    * Gói tin SYN-ACK chứa số thứ tự của client (sequence number) cộng thêm 1, để xác nhận việc nhận được gói tin SYN từ client và đồng thời cho biết nó sẵn sàng thiết lập kết nối.
    
    * Server cũng gửi số thứ tự của riêng nó (server's sequence number) đến client, để client có thể xác nhận khi gửi gói tin ACK trong bước tiếp theo.

* **Bước 3: Client gửi ACK (Acknowledgment)**:

  * Sau khi client nhận được gói tin SYN-ACK từ server, nó sẽ gửi lại một gói tin ACK đến server.
  
  * Gói tin ACK này chứa số thứ tự của server cộng thêm 1, xác nhận rằng client đã nhận được gói tin SYN-ACK từ server.
  
  * Khi server nhận được gói tin ACK này từ client, quá trình three-way handshake hoàn tất và kết nối TCP được thiết lập.

![](/img/threewayshake.png)


Thông qua quá trình này, client và server đã xác nhận và đồng ý thiết lập kết nối TCP, sẵn sàng truyền dữ liệu hai chiều giữa nhau. Mô hình ba bước này giúp đảm bảo tính toàn vẹn và đúng đắn của kết nối, đồng thời giảm thiểu khả năng xảy ra lỗi trong quá trình thiết lập kết nối.

### 4. Quá trình chấm dứt kết nối TCP (TCP teardown)

Quá trình chấm dứt kết nối TCP là quá trình quản lý và điều khiển việc ngắt kết nối một cách an toàn và đồng bộ giữa hai đầu kết nối.

Dưới đây là giải thích chi tiết về quá trình này, với ví dụ là khi client khởi tạo quá trình chấm dứt kết nối:

* **Bước 1: Client gửi FIN (Finish)**:

  * Khi client muốn kết thúc kết nối TCP, nó gửi một gói tin FIN đến server.
  
  * Gói tin FIN này chứa số thứ tự của client, tương tự như khi thiết lập kết nối.

* **Bước 2: Server gửi ACK (Acknowledgment)**:

  * Sau khi server nhận được gói tin FIN từ client, nó gửi lại một gói tin ACK để xác nhận việc nhận được gói tin FIN từ client.

  * Gói tin ACK này chứa số thứ tự của client cộng thêm 1.

* **Bước 3: Server gửi FIN (Finish)**:

  * Khi server đã hoàn thành việc truyền dữ liệu của mình, nó cũng gửi một gói tin FIN đến client.

  * Gói tin FIN này chứa số thứ tự của server.

* **Bước 4: Client gửi ACK (Acknowledgment)**:

  * Khi client nhận được gói tin FIN từ server, nó gửi lại một gói tin ACK để xác nhận việc nhận được gói tin FIN từ server.

  * Gói tin ACK này chứa số thứ tự của server cộng thêm 1.

Sau bước này, kết nối TCP đã được chấm dứt. Tuy nhiên, để đảm bảo rằng tất cả các gói tin cuối cùng đã đến đích một cách an toàn, bên gửi ACK cuối cùng (trong trường hợp này là client) sẽ tiếp tục ở trạng thái time-wait. Trong thời gian này, bên đó sẽ đợi một khoảng thời gian (theo chuẩn RFC 793 là hai phút cho mỗi gói tin ACK và bất kỳ gói tin FIN mới nào) trước khi đóng kết nối hoàn toàn và giải phóng tài nguyên liên quan đến kết nối TCP.

![](/img/teardown.png)

Quá trình này đảm bảo rằng các bên trong kết nối TCP có thể kết thúc và giải phóng tài nguyên một cách an toàn, đồng thời đảm bảo tính toàn vẹn và đúng đắn của dữ liệu truyền qua mạng.

### 5. Cấu trúc header của TCP

Thông thường, header của một gói tin TCP chứa các thông tin cần thiết cho việc kết nối và truyền dữ liệu với giao thức Điều khiển Truyền tải (TCP). Dữ liệu trong header này, bao gồm các thông tin điều khiển, đi trước phần dữ liệu payload sẽ được truyền đi và thường có kích thước là 20 byte (160 bit). Sau đó là có thể là thêm tối đa 40 byte (320 bit) thông tin bổ sung, đây là tùy chọn và không được sử dụng trong tất cả các gói tin.

Cấu trúc chi tiết của header TCP như sau:

![](/img/headerTCP.png)


1. **Source Port (Cổng nguồn)** - 16 bits:

   * Xác định số cổng của thiết bị gửi.

2. **Destination Port (Cổng đích)** - 16 bits:

    * Xác định số cổng của thiết bị nhận.

3. **Sequence Number (Số thứ tự)** - 32 bits:

   * Chỉ ra số thứ tự của byte đầu tiên trong dữ liệu gửi đi, hoặc được sử dụng khi thiết lập hoặc chấm dứt kết nối.
   
   * Dùng để xác thực và sắp xếp các đoạn dữ liệu sau khi truyền.

4. **Acknowledgment Number (Số ACK)** - 32 bits:

    * Chứa số thứ tự kế tiếp mà thiết bị gửi mong đợi nhận được.
    
    * Có một cờ ACK trong trường "Flags" là điều kiện tiên quyết để hợp lệ.

5. **Data Offset (Độ lệch)** - 4 bits:

    * Chỉ định độ dài của header TCP tính bằng từ 32-bit, để xác định điểm bắt đầu của dữ liệu gửi.
    

    * Điểm bắt đầu này thay đổi từng đoạn vì có trường "Options" có độ lớn thay đổi.
6. **Reserved (Được dự trữ)** - 6 bits:

    * Được dành để sử dụng trong tương lai theo RFC 793 và hiện tại không được sử dụng. Trường này luôn phải thiết lập bằng 0.

7. **Flags (Cờ)** - 6 bits:

   * Có sáu bit đơn lẻ khả dụng trong trường "Flags", cho phép các hành động TCP khác nhau để tổ chức giao tiếp và xử lý dữ liệu.

   * Các cờ sau có thể được thiết lập hoặc không được thiết lập cho các hành động này:

     * ``URG``: Cờ "Urgent" thông báo cho ứng dụng TCP rằng dữ liệu cần được xử lý ngay lập tức đến con trỏ "Urgent" được đặt (xem trên).

     * ``ACK``: Kết hợp với số ACK, cờ ACK xác nhận việc nhận gói tin TCP. Nếu cờ không được thiết lập, số xác nhận cũng không hợp lệ.

     * ``PSH``: Cờ "Push" đảm bảo rằng một đoạn TCP được đẩy ngay lập tức mà không cần gửi đến bộ nhớ đệm của người gửi và người nhận.

     * ``RST``: Nếu xảy ra lỗi trong quá trình truyền, có thể sử dụng một gói tin TCP với cờ RST để thiết lập lại kết nối.

     * ``SYN``: Các thông điệp có cờ SYN được thiết lập là bước đầu tiên trong ba bước bắt tay, có nghĩa là chúng khởi động kết nối.

     * ``FIN``: Cờ "Finish" thông báo cho bên kia rằng bên gửi đang kết thúc việc truyền dữ liệu.

8. **Window Size (Kích thước cửa sổ)** - 16 bits:

   * Trường này xác định số byte mà bên gửi sẵn sàng nhận.
   
9. **Checksum (Kiểm tra dư)** - 16 bits:

   * Giao thức TCP có thể phát hiện lỗi truyền. Kiểm tra dư được tính từ header, dữ liệu payload và pseudo-header để đảm bảo điều này.

10. **Urgent Pointer (Con trỏ cấp thiết)** - 16 bits:

    * Con trỏ cấp thiết chỉ ra vị trí byte đầu tiên sau dữ liệu payload cần được xử lý ngay lập tức. Do đó, trường này chỉ có giá trị và quan trọng nếu cờ URG được thiết lập.

11. **Options (Tùy chọn)** - 0 - 320 bits:

    * Sử dụng trường Options nếu bạn muốn bao gồm các chức năng TCP không thuộc header chung, ví dụ như định nghĩa kích thước đoạn tối đa.
    
    * Độ dài của các tùy chọn luôn phải là bội số của 32-bit, nếu không sẽ cần phải sử dụng lót bit 0.

## II. Giao thức UDP

### 1. Giao thức UDP là gì ?

Giao thức User Datagram Protocol (UDP) là một giao thức **cho phép gửi các datagram mà không cần thiết lập kết nối trong các mạng dựa trên IP**. Để cung cấp các dịch vụ mong muốn đến các máy chủ đích, nó sử dụng các cổng được liệt kê là một trong những thành phần cốt lõi trong header của UDP. Giống như nhiều giao thức mạng khác, UDP thuộc gia đình các giao thức Internet, nơi nó được phân loại như là một trung gian giữa lớp mạng và lớp ứng dụng ở mức độ vận chuyển

Bằng cách sử dụng UDP, một ứng dụng có thể gửi thông tin một cách rất nhanh chóng, vì không cần thiết lập kết nối với bên nhận và không cần phải chờ phản hồi. Tuy nhiên, nó không có đảm bảo rằng các gói tin sẽ đến đích một cách hoàn chỉnh và theo đúng thứ tự mà chúng đã được gửi đi. Ngoài ra, giao thức cũng không cung cấp bảo vệ chống lại sự can thiệp hoặc truy cập bởi các bên thứ ba. Tuy nhiên, các gói tin lỗi có thể được phát hiện thông qua một checksum tùy chọn (bắt buộc trong IPv6).

UDP thường được sử dụng trong các ứng dụng yêu cầu truyền tải nhanh và có thể chấp nhận mất mát dữ liệu nhất định, ví dụ như các ứng dụng truyền phát trực tiếp (streaming), trò chơi trực tuyến, hoặc ứng dụng VoIP (Voice over IP).

### 2. Các đặc tính của UDP

Để hiểu cách truyền gói tin hoạt động chi tiết với giao thức này, có ích nếu chúng ta xem xét kỹ các đặc tính của User Datagram Protocol (UDP).

1. **UDP không yêu cầu kết nối (connectionless)**: Việc truyền dữ liệu qua UDP được đặc trưng bởi việc không cần thiết lập kết nối trước đó giữa người gửi và người nhận. Các gói tin được gửi tới địa chỉ IP mong muốn, chỉ định cổng đích mà không cần máy tính phía sau phải phản hồi lại. Tuy nhiên, nếu các gói tin cần được gửi lại cho người nhận, header UDP có thể tùy chọn chứa cả cổng nguồn.

2. **UDP sử dụng cổng (ports)**: Tương tự như TCP, UDP sử dụng các cổng để đảm bảo các gói tin được chuyển đến đúng giao thức hay ứng dụng mong muốn trên hệ thống đích. Các cổng được định nghĩa bằng các số theo mẫu được chứng minh, với các số từ 0 đến 1023 được gán cho các dịch vụ cố định.

3. **UDP cho phép giao tiếp nhanh, không có độ trễ**: Giao thức vận chuyển này phù hợp cho việc truyền tải dữ liệu nhanh chóng do không cần thiết lập kết nối. Điều này cũng phản ánh từ việc mất mát của các gói tin cá nhân chỉ ảnh hưởng đến chất lượng của truyền tải. Ngược lại, với kết nối TCP, các gói tin bị mất sẽ được yêu cầu gửi lại, dẫn đến toàn bộ quá trình truyền tải bị dừng lại.

4. **UDP không đảm bảo bảo mật và tính toàn vẹn của dữ liệu**: Sự thiếu đi sự xác thực lẫn nhau giữa người gửi và người nhận đảm bảo tốc độ truyền tải tuyệt vời của UDP - tuy nhiên, giao thức này không thể đảm bảo sự hoàn chỉnh hay an toàn của các gói tin dữ liệu. Thứ tự chính xác của các gói tin được gửi cũng không được đảm bảo. Vì lý do này, các dịch vụ sử dụng UDP phải tự cung cấp các biện pháp riêng để sửa chữa hoặc bảo vệ dữ liệu.

### 3. Cấu trúc header của UDP

Như các giao thức khác, các gói tin UDP bao gồm một phần header và dữ liệu người dùng thực tế. Header UDP chứa tất cả thông tin cần thiết cho việc truyền dữ liệu bằng giao thức vận chuyển này và làm cho gói tin UDP có thể được nhận dạng. **Chia thành hai khối 32-bit** với bốn trường dữ liệu khác nhau, cấu trúc như sau:

![](/img/headerUDP.png)


Các **16 bit đầu tiên** của vùng header cho biết cổng nguồn từ đó gói tin dữ liệu tương ứng được gửi đi. Người nhận cần thông tin này để có thể phản hồi lại gói tin. Do **UDP là một giao thức không cần thiết lập kết nối** và không có sự trao đổi giữa người gửi và người nhận, trường này là **tùy chọn**. Do đó, giá trị "0" thường được thiết lập ở đây.

Ở trường tiếp theo, **cổng đích** và do đó dịch vụ cần truy cập được chỉ định. Khác với cổng nguồn, thông tin này là bắt buộc, nếu không datagram không thể được gán cho đúng.

Trường độ dài xác định chiều dài của datagram. Nó bao gồm độ dài của header (8 byte) và kích thước của dữ liệu người dùng (tối đa lý thuyết: 65,535 byte). Khi sử dụng IPv4, giới hạn thực tế cho dữ liệu người dùng là 65,507 byte - sau khi trừ đi header IP và UDP. Trong IPv6, các gói tin (được gọi là jumbograms) vượt quá giới hạn tối đa cũng có thể xảy ra. Theo [RFC 2675](https://datatracker.ietf.org/doc/html/rfc2675), giá trị của trường độ dài được thiết lập thành "0" trong trường hợp như vậy.

Header UDP kết thúc bằng trường băm kiểm tra (checksum), được sử dụng để phát hiện lỗi trong quá trình truyền. Nhờ đó, bất kỳ sự can thiệp nào vào dữ liệu được truyền cũng có thể được phát hiện.

Yuy nhiên, các gói tin tương ứng sẽ bị loại bỏ mà không cần yêu cầu gửi lại. Để tính toán checksum, các phần của: 
* header UDP
* Dữ liệu người dùng
* cũng như **pseudo-header** (chứa thông tin header IP) đều được bao gồm.

Checksum là tùy chọn trong IPv4, nhưng được sử dụng mặc định bởi hầu hết các ứng dụng. Nếu bỏ qua nó, trường này cũng sẽ có giá trị "0". Nếu UDP được sử dụng kết hợp với IPv6, checksum là bắt buộc.

# END