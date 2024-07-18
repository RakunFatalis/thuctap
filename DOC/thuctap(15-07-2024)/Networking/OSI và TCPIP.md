# Mô hình OSI, TCP/IP

# MỤC LỤC
- [Mô hình OSI, TCP/IP](#mô-hình-osi-tcpip)
- [MỤC LỤC](#mục-lục)
  - [I. Mô hình OSI](#i-mô-hình-osi)
    - [1. Mô hình OSI là gì ?](#1-mô-hình-osi-là-gì-)
    - [2. Các lớp của mô hình OSI](#2-các-lớp-của-mô-hình-osi)
  - [II. Mô hình TCP/IP](#ii-mô-hình-tcpip)
    - [1. Mô hình TCP/IP là gì ?](#1-mô-hình-tcpip-là-gì-)
    - [2. Các lớp của mô hình TCP/IP](#2-các-lớp-của-mô-hình-tcpip)
  - [Mô hình OSI hay mô hình TCP/IP](#mô-hình-osi-hay-mô-hình-tcpip)
  - [TỔNG KẾT](#tổng-kết)


## I. Mô hình OSI

### 1. Mô hình OSI là gì ?

Mô hình Kết nối Hệ thống Mở (OSI) là một khung khái niệm được sử dụng để hiểu và chuẩn hóa các chức năng của một hệ thống viễn thông hoặc máy tính mà không cần quan tâm đến cấu trúc nội bộ và công nghệ cơ bản của nó. Mục tiêu của nó là cho phép các hệ thống giao tiếp đa dạng có thể giao tiếp với nhau bằng cách sử dụng các giao thức chuẩn.


### 2. Các lớp của mô hình OSI

Mô hình Kết nối giữa các hệ thống mở (Open Systems Interconnection – OSI) được phát triển bởi Tổ chức tiêu chuẩn hóa quốc tế và các tổ chức khác vào cuối những năm 1970. Mô hình này được ra mắt dưới dạng đầu tiên vào năm 1984 với tên ISO 7498, và phiên bản hiện tại là ISO/IEC 7498-1:1994. Dưới đây là 7 lớp của mô hình.

![](/img/OSI7Layers.png)

* **Lớp vật lý (Physical Layer)**

    Lớp Vật lý là lớp thấp nhất trong mô hình OSI và nó chịu trách nhiệm cho việc truyền tải dữ liệu thực tế giữa các thiết bị. Dưới đây là một số điểm chính về lớp vật lý:

    1. **Thiết bị vật lý**: Lớp này bao gồm các thiết bị vật lý tham gia vào quá trình truyền dữ liệu như cáp, bộ chuyển mạch (switch), bộ định tuyến (router), và các thành phần phần cứng khác. Các thiết bị này chịu trách nhiệm cho việc kết nối vật lý giữa các thiết bị mạng.

    2. **Chuyển đổi dữ liệu**: Tại lớp vật lý, dữ liệu được chuyển đổi thành một chuỗi các bit, là các dãy số 1 và 0. Chuỗi bit này đại diện cho thông tin được truyền đi qua các phương tiện vật lý.

    3. **Chuẩn tín hiệu**: Để đảm bảo rằng dữ liệu được truyền đi một cách chính xác, cả hai thiết bị phải đồng ý về một quy ước tín hiệu. Quy ước này xác định cách mà các số 1 và 0 sẽ được phân biệt trên cả hai thiết bị. Điều này bao gồm việc xác định mức điện áp hoặc các tín hiệu ánh sáng để biểu thị các bit 1 và 0.

    3. **Đồng bộ hóa**: Lớp vật lý cũng phải đảm bảo rằng cả hai thiết bị đang hoạt động đồng bộ với nhau. Điều này bao gồm việc đảm bảo rằng tín hiệu truyền đi được nhận và giải mã một cách chính xác tại đích đến.

    ![](/img/physicalplayer.png)

* **Lớp liên kết dữ liệu (Data link Layer)**

    Lớp Liên kết Dữ liệu là lớp thứ hai trong mô hình OSI và chịu trách nhiệm cho việc truyền dữ liệu giữa hai thiết bị trên cùng một mạng. Dưới đây là các điểm chính về lớp liên kết dữ liệu:

    1. **Chức năng chính**: Lớp liên kết dữ liệu nhận các gói dữ liệu từ lớp mạng và chia chúng thành các khung (frames) nhỏ hơn. Mỗi khung chứa dữ liệu cũng như thông tin kiểm soát để đảm bảo truyền dữ liệu an toàn và hiệu quả.

    2. **Kiểm soát lưu lượng (Flow Control)**: Lớp này điều chỉnh tốc độ truyền dữ liệu giữa hai thiết bị để đảm bảo rằng thiết bị nhận có thể xử lý dữ liệu mà không bị quá tải.

    3. **Kiểm soát lỗi (Error Control)**: Lớp liên kết dữ liệu phát hiện và sửa chữa các lỗi xảy ra trong quá trình truyền dữ liệu. Nó sử dụng các phương pháp như kiểm tra tuần hoàn (CRC - Cyclic Redundancy Check) để đảm bảo tính toàn vẹn của dữ liệu.

    4. **Địa chỉ MAC (Media Access Control)**: Mỗi thiết bị trên mạng có một địa chỉ MAC duy nhất, và lớp liên kết dữ liệu sử dụng địa chỉ này để định danh các thiết bị khi truyền dữ liệu. Điều này giúp đảm bảo rằng dữ liệu được gửi đến đúng thiết bị.

    5. **Phân chia lớp:** Lớp liên kết dữ liệu thường được chia thành hai phân lớp chính:

       * **Lớp điều khiển truy cập môi trường** (MAC - Media Access Control): Quản lý quyền truy cập vào phương tiện truyền thông vật lý, điều này có nghĩa là nó quyết định khi nào một thiết bị có thể truyền dữ liệu trên mạng.


       * **Lớp điều khiển liên kết logic** (LLC - Logical Link Control): Chịu trách nhiệm cho việc phân loại và điều khiển luồng dữ liệu, cũng như phát hiện và sửa chữa lỗi. 

    6. **Khác biệt với Lớp Mạng (Network Layer)**: Trong khi lớp liên kết dữ liệu quản lý việc truyền dữ liệu giữa hai thiết bị trên cùng một mạng (intra-network), lớp mạng chịu trách nhiệm cho việc định tuyến dữ liệu giữa các mạng khác nhau (inter-network).

    ![](/img/datalinklayer.png)

* **Lớp mạng (Network layer)**

    Lớp Mạng là lớp thứ ba trong mô hình OSI và chịu trách nhiệm cho việc tạo lập, vận chuyển và lắp ráp các gói dữ liệu (packets) giữa hai mạng khác nhau. Dưới đây là các điểm chính về lớp mạng:

    1. **Tạo gói dữ liệu (Packets Creation)**: Lớp mạng nhận các đoạn dữ liệu (segments) từ lớp giao vận (transport layer) và chia chúng thành các đơn vị nhỏ hơn gọi là gói dữ liệu (packets). Điều này giúp dữ liệu dễ dàng được quản lý và truyền tải qua mạng.

    2. **Vận chuyển gói dữ liệu (Packets Transport)**: Lớp mạng chịu trách nhiệm cho việc vận chuyển các gói dữ liệu từ thiết bị gửi đến thiết bị nhận. Quá trình này bao gồm việc định tuyến (routing) các gói qua các mạng trung gian cho đến khi chúng đến được đích cuối cùng.

    3. **Lắp ráp gói dữ liệu (Packets Assembly)**: Trên thiết bị nhận, lớp mạng sẽ lắp ráp lại các gói dữ liệu thành các đoạn dữ liệu ban đầu, giúp dữ liệu có thể được xử lý bởi các lớp cao hơn.

    4. **Định tuyến (Routing)**: Một trong những chức năng quan trọng nhất của lớp mạng là tìm kiếm con đường vật lý tốt nhất để dữ liệu có thể đến được đích. Quá trình định tuyến liên quan đến việc xác định và sử dụng các tuyến đường (routes) hiệu quả nhất thông qua các thiết bị trung gian như bộ định tuyến (routers).

    5. **Giao thức lớp mạng (Network Layer Protocols):** Các giao thức chính hoạt động ở lớp mạng bao gồm:

        * **IP (Internet Protocol)**: Giao thức chính của Internet, chịu trách nhiệm định địa chỉ và định tuyến các gói dữ liệu.

        * **ICMP (Internet Control Message Protocol)**: Sử dụng để gửi các thông điệp lỗi và các thông điệp điều khiển khác liên quan đến hoạt động của mạng.

        * **IGMP (Internet Group Management Protocol)**: Được sử dụng để quản lý các thành viên trong các nhóm multicast, cho phép các thiết bị tham gia và rời khỏi các nhóm này.

        * **IPsec (Internet Protocol Security)**: Một bộ giao thức được sử dụng để bảo mật các gói dữ liệu IP thông qua việc mã hóa và xác thực.

    **Vai trò của Lớp Mạng:**

    Truyền dữ liệu giữa các mạng khác nhau: Lớp mạng đóng vai trò quan trọng trong việc truyền dữ liệu giữa các mạng khác nhau (inter-network communication). Nếu hai thiết bị đang giao tiếp nằm trong cùng một mạng, lớp mạng không cần thiết.

    Đảm bảo truyền dữ liệu hiệu quả: Bằng cách chia nhỏ dữ liệu thành các gói và tìm đường đi tối ưu, lớp mạng đảm bảo rằng dữ liệu được truyền tải một cách hiệu quả và đáng tin cậy từ nguồn đến đích.

    ![](/img/networklayer.png)

* **Lớp truyền tải (Transport Layer)**

    Lớp Giao Vận là lớp thứ tư trong mô hình OSI và chịu trách nhiệm cho việc giao tiếp từ đầu đến cuối giữa hai thiết bị. Dưới đây là các điểm chính về lớp giao vận:
    
    * **Phân đoạn (Segment)**: Lớp giao vận nhận dữ liệu từ lớp phiên (session layer) và chia dữ liệu này thành các đoạn nhỏ hơn gọi là phân đoạn (segments) trước khi gửi chúng xuống lớp mạng (network layer). Quá trình này giúp quản lý và truyền tải dữ liệu dễ dàng hơn qua mạng.

    * **Vận chuyển (Transport)**: Lớp giao vận đảm bảo rằng các phân đoạn dữ liệu được truyền từ nguồn đến đích một cách hiệu quả và đáng tin cậy. Nó chịu trách nhiệm thiết lập, duy trì và kết thúc các kết nối truyền thông.

    * **Lắp ráp lại (Reassembly)**: Trên thiết bị nhận, lớp giao vận chịu trách nhiệm lắp ráp lại các phân đoạn thành dữ liệu ban đầu để lớp phiên có thể xử lý. Quá trình này đảm bảo rằng dữ liệu được tái tạo đúng cách tại đích.

    **Các Chức năng Chính của Lớp Giao Vận**:
    
    * **Kiểm soát lưu lượng (Flow Control)**: Lớp giao vận điều chỉnh tốc độ truyền dữ liệu để đảm bảo rằng một thiết bị gửi có kết nối nhanh không làm quá tải thiết bị nhận có kết nối chậm. Điều này đảm bảo rằng dữ liệu được truyền tải một cách hiệu quả mà không gây ra mất mát hoặc hỏng dữ liệu.

    * **Kiểm soát lỗi (Error Control)**: Lớp giao vận thực hiện kiểm soát lỗi ở phía nhận bằng cách đảm bảo rằng dữ liệu nhận được là đầy đủ và chính xác. Nếu có lỗi hoặc thiếu dữ liệu, lớp giao vận sẽ yêu cầu truyền lại.

    **Các Giao thức của Lớp Giao Vận:**

    * **Transmission Control Protocol (TCP)**: TCP là một giao thức kết nối, đảm bảo rằng tất cả các phân đoạn được truyền tải một cách đáng tin cậy và theo đúng thứ tự. TCP thực hiện kiểm soát lưu lượng và kiểm soát lỗi chặt chẽ, đảm bảo rằng dữ liệu đến đích một cách toàn vẹn và không bị mất mát.

    * **User Datagram Protocol (UDP)**: UDP là một giao thức không kết nối, cho phép truyền tải dữ liệu nhanh chóng nhưng không đảm bảo tính toàn vẹn và thứ tự của dữ liệu như TCP. UDP phù hợp cho các ứng dụng yêu cầu tốc độ cao và có thể chấp nhận một mức độ mất mát dữ liệu, như streaming video hoặc audio.

    ![](/img/transportlayer.png)

* **Lớp phiên (Session Layer)**

    Lớp Phiên là lớp thứ năm trong mô hình OSI và chịu trách nhiệm cho việc mở và đóng phiên giao tiếp giữa hai thiết bị. Dưới đây là các điểm chính về lớp phiên:

    * **Phiên giao tiếp (Session of Communication)**: Lớp phiên quản lý các phiên giao tiếp giữa các thiết bị. Phiên bắt đầu khi việc giao tiếp được mở và kết thúc khi việc giao tiếp được đóng. Khoảng thời gian giữa lúc mở và đóng phiên được gọi là phiên (session).

    * **Mở và đóng phiên (Opening and Closing Sessions)**: Lớp phiên đảm bảo rằng phiên được mở đủ lâu để truyền tất cả dữ liệu đang được trao đổi, và sau đó nhanh chóng đóng phiên để tránh lãng phí tài nguyên. Điều này đảm bảo rằng các nguồn tài nguyên hệ thống không bị chiếm dụng không cần thiết.

    * **Đồng bộ hóa chuyển dữ liệu với điểm kiểm tra (Checkpoints Synchronization)**: Lớp phiên cũng đồng bộ hóa việc truyền dữ liệu bằng cách đặt các điểm kiểm tra (checkpoints). Ví dụ, nếu một tệp 100 megabyte đang được truyền, lớp phiên có thể đặt điểm kiểm tra mỗi 5 megabyte. Trong trường hợp bị ngắt kết nối hoặc gặp sự cố sau khi đã truyền được 52 megabyte, phiên có thể được tiếp tục từ điểm kiểm tra cuối cùng, tức là chỉ cần truyền thêm 50 megabyte dữ liệu nữa. Nếu không có các điểm kiểm tra, toàn bộ quá trình truyền dữ liệu sẽ phải bắt đầu lại từ đầu.

    **Vai trò của Lớp Phiên:**
      
    * **Quản lý phiên (Session Management)**: Đảm bảo rằng các phiên giao tiếp được thiết lập, duy trì và kết thúc đúng cách. Điều này bao gồm việc đồng bộ hóa và quản lý thời gian hoạt động của phiên.

    * **Đồng bộ hóa và phục hồi (Synchronization and Recovery)**: Cung cấp cơ chế đồng bộ hóa dữ liệu bằng các điểm kiểm tra, giúp phục hồi truyền dữ liệu trong trường hợp gặp sự cố. Điều này rất quan trọng để đảm bảo rằng dữ liệu không bị mất và quá trình truyền dữ liệu diễn ra một cách trơn tru.

    ![](/img/sessionlayer.png)

* **Lớp Trình Bày (Presentation Layer)**

    Lớp Trình Bày là lớp thứ sáu trong mô hình OSI và chịu trách nhiệm chuẩn bị dữ liệu để có thể sử dụng bởi lớp ứng dụng (application layer). Nói cách khác, lớp trình bày làm cho dữ liệu trở nên dễ sử dụng cho các ứng dụng. Dưới đây là các điểm chính về lớp trình bày:

    * **Dịch (Translation)**: Lớp trình bày chịu trách nhiệm dịch dữ liệu đến từ các phương pháp mã hóa khác nhau. Khi hai thiết bị giao tiếp sử dụng các phương pháp mã hóa khác nhau, lớp trình bày dịch dữ liệu đến thành một cú pháp mà lớp ứng dụng của thiết bị nhận có thể hiểu được.     

    * **Mã hóa (Encryption)**: Nếu các thiết bị giao tiếp qua một kết nối mã hóa, lớp trình bày chịu trách nhiệm thêm mã hóa vào dữ liệu ở phía gửi và giải mã dữ liệu ở phía nhận để lớp ứng dụng có thể nhận được dữ liệu không mã hóa, dễ đọc.

    * **Nén (Compression)**: Lớp trình bày cũng chịu trách nhiệm nén dữ liệu mà nó nhận từ lớp ứng dụng trước khi chuyển đến lớp phiên. Việc nén giúp cải thiện tốc độ và hiệu suất truyền thông bằng cách giảm thiểu lượng dữ liệu cần truyền.

    **Các Chức năng Chính của Lớp Trình Bày:**

    * **Chuẩn bị dữ liệu (Data Preparation)**: Chuẩn bị dữ liệu để lớp ứng dụng có thể tiêu thụ một cách hiệu quả. Điều này bao gồm việc dịch, mã hóa và nén dữ liệu.
    
    * **Dịch (Translation)**: Đảm bảo rằng dữ liệu được chuyển đổi thành định dạng mà lớp ứng dụng của thiết bị nhận có thể hiểu được. Điều này rất quan trọng khi các thiết bị sử dụng các hệ thống mã hóa khác nhau.

    * **Mã hóa và giải mã (Encryption and Decryption)**: Bảo vệ dữ liệu bằng cách mã hóa nó trước khi truyền và giải mã dữ liệu khi nhận. Điều này giúp bảo vệ dữ liệu khỏi việc bị truy cập trái phép trong quá trình truyền tải.

    * **Nén và giải nén (Compression and Decompression)**: Giảm kích thước dữ liệu trước khi truyền để cải thiện tốc độ và hiệu quả của truyền thông. Khi dữ liệu đến thiết bị nhận, lớp trình bày sẽ giải nén dữ liệu để nó có thể được sử dụng bởi các lớp cao hơn.

    ![](/img/presentationlayer.png)

* **Lớp Ứng Dụng (Application Layer)**

    Lớp Ứng Dụng là lớp thứ bảy và cao nhất trong mô hình OSI, chịu trách nhiệm tương tác trực tiếp với dữ liệu từ người dùng. Dưới đây là các điểm chính về lớp ứng dụng:

    * **Tương tác với dữ liệu người dùng (Interacting with User Data)**: Lớp ứng dụng là lớp duy nhất tương tác trực tiếp với dữ liệu từ người dùng. Các ứng dụng phần mềm như trình duyệt web và ứng dụng email dựa vào lớp ứng dụng để bắt đầu các giao tiếp.

    * **Ứng dụng khách không thuộc về lớp ứng dụng (Client Software Applications)**: Cần làm rõ rằng các ứng dụng phần mềm khách không phải là một phần của lớp ứng dụng; thay vào đó, lớp ứng dụng chịu trách nhiệm cho các giao thức và việc xử lý dữ liệu mà phần mềm dựa vào để trình bày dữ liệu có ý nghĩa cho người dùng.

    * **Yêu cầu và trả về nội dung (Content Requested and Returned)**: Lớp ứng dụng đảm bảo rằng nội dung được yêu cầu bởi người dùng được lấy và trả về trong định dạng yêu cầu. Điều này có nghĩa là lớp ứng dụng quản lý các yêu cầu và phản hồi dữ liệu giữa người dùng và hệ thống mạng.

    **Các Chức năng Chính của Lớp Ứng Dụng:**

    * Khởi tạo giao tiếp (Initiating Communications): Bắt đầu các kết nối và giao tiếp dựa trên yêu cầu của ứng dụng người dùng. Ví dụ, khi người dùng nhập một URL vào trình duyệt web, lớp ứng dụng chịu trách nhiệm tạo ra yêu cầu HTTP để lấy nội dung trang web.

    * Quản lý giao thức (Managing Protocols): Xử lý các giao thức cần thiết cho việc truyền tải dữ liệu. Điều này bao gồm các giao thức như HTTP, SMTP, FTP và nhiều giao thức khác được sử dụng để truyền tải dữ liệu ứng dụng.

    * Trình bày dữ liệu có ý nghĩa (Presenting Meaningful Data): Đảm bảo rằng dữ liệu được truyền tải và trình bày theo cách mà người dùng có thể hiểu và sử dụng. Điều này bao gồm việc định dạng lại dữ liệu theo yêu cầu của ứng dụng phần mềm.

    **Các Giao thức của Lớp Ứng Dụng:**

    * HTTP (Hypertext Transfer Protocol): Giao thức chính cho việc truyền tải các trang web và nội dung trên internet. HTTP quản lý các yêu cầu và phản hồi giữa trình duyệt web và máy chủ web.

    * SMTP (Simple Mail Transfer Protocol): Một trong những giao thức chính cho việc truyền tải email. SMTP quản lý việc gửi email từ máy khách đến máy chủ email và giữa các máy chủ email với nhau.
    
    * FTP (File Transfer Protocol): Giao thức dùng để truyền tải tệp tin qua mạng. FTP cho phép người dùng tải lên và tải xuống tệp tin từ một máy chủ.

## II. Mô hình TCP/IP

### 1. Mô hình TCP/IP là gì ?

TCP/ IP (Transmission Control Protocol/ Internet Protocol - Giao thức điều khiển truyền nhận/ Giao thức liên mạng), là một bộ giao thức trao đổi thông tin được sử dụng để truyền tải và kết nối các thiết bị trong mạng Internet. TCP/IP được phát triển để mạng được tin cậy hơn cùng với khả năng phục hồi tự động.


### 2. Các lớp của mô hình TCP/IP

Mô hình TCP/IP bao gồm bốn lớp chính, mỗi lớp đảm nhận các chức năng cụ thể trong quá trình truyền thông mạng. Đây là các lớp của mô hình TCP/IP:

![](/img/tcpiplayer.png)


* **Lớp truy cập mạng (Network Access Layer)**

    Đôi khi được gọi là lớp liên kết dữ liệu (Data Link Layer), là lớp trong mô hình mạng OSI hoặc TCP/IP và có các chức năng cụ thể sau:

    * **Quản lý truyền và nhận khung dữ liệu**: Lớp này tổ chức việc gửi và nhận các khung dữ liệu trên một mạng cụ thể. Khung dữ liệu là đơn vị dữ liệu nhỏ nhất mà lớp này xử lý, thường bao gồm các trường như địa chỉ vật lý (MAC address), kiểm tra lỗi và các thông tin khác cần thiết để điều khiển việc truyền dữ liệu.

    * **Phần cứng vật lý liên quan đến truyền dẫn mạng:** Lớp này tương ứng với các thiết bị vật lý tham gia vào truyền dẫn mạng như hub, modem, cáp và dây cáp. Các thiết bị này tham gia vào việc truyền và nhận dữ liệu trên mạng.

    * **Giao thức giải quyết địa chỉ (ARP)**: ARP là một phần của lớp truy cập mạng và hỗ trợ giao thức IP trong việc định tuyến các gói dữ liệu trên cùng một mạng vật lý. ARP giúp ánh xạ địa chỉ IP sang địa chỉ MAC trên cùng một mạng, từ đó cho phép các thiết bị trong mạng tìm ra nhau và giao tiếp trực tiếp.

* **Lớp Internet (Internet Layer)**

    Đôi khi được gọi là lớp mạng (Network Layer), là một trong các lớp trong mô hình mạng OSI hoặc TCP/IP, với các chức năng chính sau:

    * **Đảm bảo giao tiếp giữa các mạng khác nhau**: Lớp Internet chịu trách nhiệm đảm bảo việc gửi dữ liệu từ một thiết bị đến một thiết bị đích, có thể nằm trên các mạng khác nhau. Điều này đòi hỏi lớp Internet phải quyết định xem gói dữ liệu sẽ được giao bằng cách nào.

    * **Giao thức Internet Protocol (IP)**: IP là giao thức chủ yếu hoạt động tại lớp này. Nó gán địa chỉ IP cho các gói dữ liệu để chỉ ra vị trí của người gửi và người nhận. IP cho phép giao tiếp giữa các mạng khác nhau bằng cách định tuyến các gói dữ liệu từ mạng gửi đến mạng nhận.

    * **Giao thức Internet Control Message Protocol (ICMP)**: ICMP là giao thức phụ trợ hoạt động trong lớp Internet. Nó chia sẻ thông tin lỗi và cập nhật trạng thái của các gói dữ liệu. ICMP rất hữu ích trong việc phát hiện và sửa chữa các lỗi mạng. Nó thông báo về các gói dữ liệu bị mất, các vấn đề về kết nối mạng, và các gói dữ liệu bị chuyển hướng sang các bộ định tuyến khác.

* **Lớp giao vận (Transport Layer)**

    Lớp giao vận trong mô hình TCP/IP cung cấp hai giao thức chính là TCP và UDP để đảm bảo việc truyền tải dữ liệu đáng tin cậy hoặc hiệu suất cao tùy thuộc vào yêu cầu của ứng dụng. TCP đảm bảo độ tin cậy và sắp xếp dữ liệu, trong khi UDP tối ưu cho các ứng dụng yêu cầu hiệu suất và thời gian thực.

    Lớp giao vận trong mô hình TCP/IP đảm nhận các chức năng quan trọng sau:

    * **Đảm bảo truyền dữ liệu đáng tin cậy giữa hai hệ thống hoặc mạng**: Lớp này chịu trách nhiệm đảm bảo việc dữ liệu được truyền tải đáng tin cậy từ một điểm đến một điểm khác trên mạng.

    * **Giao thức Transmission Control Protocol (TCP)**:

      * TCP là giao thức đảm bảo việc truyền tải dữ liệu một cách đáng tin cậy tới dịch vụ đích.
    
      * TCP sử dụng các port number để xác định dịch vụ mà dữ liệu được gửi tới, thông qua các tiêu đề TCP/IP trong gói tin TCP.
    
      * TCP cung cấp các tính năng như đảm bảo thứ tự dữ liệu, kiểm tra lỗi, và tái sử dụng dữ liệu bị mất.
    
    * **Giao thức User Datagram Protocol (UDP)**:

      * UDP được sử dụng bởi các ứng dụng không cần quan tâm đến độ tin cậy của truyền tải.
      
      * Dữ liệu gửi qua UDP không được theo dõi chi tiết như khi sử dụng TCP.
      
      * UDP không thiết lập kết nối mạng, do đó thường được sử dụng cho các ứng dụng yêu cầu hiệu suất cao, như truyền dữ liệu thời gian thực như video streaming.

## Mô hình OSI hay mô hình TCP/IP

Mô hình OSI **(Open Systems Interconnection)** và mô hình TCP/IP **(Transmission Control Protocol/Internet Protocol)** là hai mô hình tham chiếu được sử dụng để mô tả và phân loại các chức năng của các giao thức mạng và các tầng của chúng. Dưới đây là một số điểm khác nhau cơ bản giữa hai mô hình này:


| Đặc điểm| Mô hình OSI| Mô hình TCP/IP|
|---------|------------|---------------|
| **Số lượng tầng**| Bao gồm 7 tầng: Physical, Data Link, Network, Transport, Session, Presentation, Application | Bao gồm 4 tầng: Network Access (Link), Internet, Transport, Application  |
| **Mục đích ban đầu**| Được thiết kế nhằm chuẩn hóa giao tiếp mạng giữa các thiết bị khác nhau một cách chi tiết và lý thuyết | Phát triển từ thực tế và sử dụng rộng rãi trong hệ thống Internet và mạng lớn |
| **Các tầng chi tiết**| Cung cấp các tầng Presentation và Session riêng biệt | Không có các tầng Presentation và Session, thay vào đó là các thư viện và API ứng dụng |
| **Phụ thuộc vào công nghệ**| Không phụ thuộc vào bất kỳ công nghệ hay giao thức cụ thể nào | Phụ thuộc vào các giao thức thực tế như IP, TCP, UDP, ICMP, ... |
| **Sử dụng trong thực tế**| Ít được sử dụng rộng rãi trong thực tế so với TCP/IP | Sử dụng rộng rãi cho Internet và các hệ thống mạng lớn |
| **Thiết kế**| Chi tiết và cụ thể, mô phỏng tất cả các khía cạnh của mạng | Đơn giản, linh hoạt và có khả năng thích ứng với các môi trường mạng |
| **Các giao thức tiêu biểu**| TCP, UDP, IP, HTTP, FTP, SMTP | IP, TCP, UDP, ICMP, DHCP, DNS |
| **Phù hợp với**| Được sử dụng trong giả lập và nghiên cứu, không gian lý thuyết | Phù hợp cho các môi trường mạng thực tế và hệ thống Internet |

## TỔNG KẾT

Mô hình OSI và TCP/IP đều cung cấp một cách để hiểu cấu trúc và hoạt động của các giao thức mạng. OSI mang tính lý thuyết và chi tiết, trong khi TCP/IP mang tính thực tiễn và sử dụng rộng rãi. Mỗi mô hình có ưu điểm và hạn chế riêng, và việc lựa chọn mô hình phù hợp phụ thuộc vào mục đích cụ thể của hệ thống mạng và ứng dụng.
