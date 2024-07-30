# Tổng quan http

# Mục lục

- [Tổng quan http](#tổng-quan-http)
- [Mục lục](#mục-lục)
  - [I. Giao thức HTTP là gì?](#i-giao-thức-http-là-gì)
  - [II. Lịch sử của HTTP](#ii-lịch-sử-của-http)
  - [III. Đặc điểm của HTTP](#iii-đặc-điểm-của-http)
- [END](#end)



## I. Giao thức HTTP là gì?

HTTP là viết tắt của HyperText Transfer Protocol, là một giao thức truyền tải siêu văn bản, giúp cho các máy tính có thể giao tiếp với nhau qua mạng. HTTP là nền tảng của World Wide Web kết nối giữa máy chủ (server) và máy khách (client) trong cùng một hệ thống mạng. Điều này cho phép chúng ta truy cập vào các trang web, tải xuống các tệp tin, xem các hình ảnh, video… Ban đầu khi được thiết kế vào những năm 90, HTTP là một giao thức linh hoạt có khả năng mở rộng theo thời gian. Giao thức này hoạt động trên nền tảng TCP/IP và thường được truyền qua kết nối mã hóa TLS để bảo vệ dữ liệu. Mặc dù về lý thuyết, bất kỳ giao thức truyền tải đáng tin cậy nào cũng có thể được áp dụng.

Với khả năng mở rộng đa dạng, HTTP không chỉ được sử dụng để tải các tài liệu siêu văn bản, mà còn để truyền tải hình ảnh, video và thậm chí để đăng tải nội dung lên máy chủ, chẳng hạn như kết quả của các biểu mẫu HTML. Ngoài ra, HTTP cũng có thể sử dụng để tải lên các phần của trang web, giúp cập nhật nội dung theo yêu cầu.

HTTP được sử dụng rộng rãi trong việc truy cập các trang web trên Internet. Khi bạn nhập một địa chỉ web vào trình duyệt, trình duyệt sẽ gửi một yêu cầu HTTP đến máy chủ web, và máy chủ web sẽ trả về một phản hồi HTTP chứa mã HTML của trang web đó. Trình duyệt sẽ đọc mã HTML và hiển thị trang web cho bạn xem. Bạn có thể thấy các yêu cầu và phản hồi HTTP bằng cách sử dụng công cụ kiểm tra mạng (network inspector) của trình duyệt.

![](/thuctap/img/http.png)


## II. Lịch sử của HTTP

Tim Berners-Lee và nhóm của ông tại CERN được ghi nhận là những người phát minh ra giao thức HTTP gốc.

* **HTTP 0.9 (1991)**
    HTTP 0.9 là phiên bản đầu tiên của giao thức HTTP, được phát triển để truyền tải các tài liệu HTML đơn giản. Đây là một giao thức rất cơ bản với chức năng chính là truyền tải dữ liệu HTML mà không hỗ trợ nhiều tính năng mở rộng.

*  **HTTP 1.0 (1996)**

    HTTP 1.0, được giới thiệu trong RFC 1945, mở rộng các khả năng của giao thức với các tính năng như tiêu đề HTTP, mã trạng thái và hỗ trợ nhiều loại phương thức yêu cầu (như GET, POST). Điều này giúp cải thiện khả năng truyền tải và quản lý dữ liệu hơn so với phiên bản trước.

* **HTTP 1.1 (1997)**

    HTTP 1.1, được quy định bởi RFC 2068 và sau đó là RFC 2616, cải tiến hiệu suất và tính năng của HTTP 1.0. Các tính năng nổi bật bao gồm kết nối duy trì (persistent connections), pipelining (tính năng cho phép gửi nhiều yêu cầu mà không cần chờ phản hồi từ máy chủ) và cải thiện cơ chế cache.

* **HTTP 2.0 (2015)**

    HTTP 2.0, được quy định trong RFC 7540, giới thiệu nhiều cải tiến quan trọng so với HTTP 1.1. Các tính năng mới bao gồm đa luồng (multiplexing), nén tiêu đề (header compression), và gửi nhiều yêu cầu và phản hồi qua một kết nối TCP duy nhất, giúp cải thiện hiệu suất và giảm độ trễ.   

* **HTTP 3.0 (HTTP/3)**

    HTTP 3.0, được phát triển dựa trên giao thức QUIC (Quick UDP Internet Connections) và đổi tên thành Hyper-Text Transfer Protocol QUIC (HTTP/3), nhằm cải thiện hiệu suất web hơn nữa. QUIC là một giao thức truyền tải dữ liệu dựa trên UDP (User Datagram Protocol) thay vì TCP, giúp giảm độ trễ và cải thiện tốc độ truyền tải dữ liệu qua mạng.

HTTP đã phát triển qua nhiều phiên bản, từ HTTP 0.9 đơn giản đến HTTP/3 với nhiều cải tiến về hiệu suất và tính năng. Mỗi phiên bản đã đóng góp vào việc nâng cao khả năng và hiệu quả của giao thức HTTP, phù hợp với nhu cầu ngày càng cao của các ứng dụng web hiện đại.

## III. Đặc điểm của HTTP

* **Tính đơn giản của HTTP**

    Giao thức HTTP được thiết kế với sự đơn giản và thân thiện đối với người đọc, ngay cả khi có sự phức tạp được tích hợp trong HTTP/2 thông qua việc đóng gói các HTTP message thành các frame. Bằng cách này, việc đọc và hiểu các thông điệp HTTP trở nên dễ dàng hơn, cung cấp khả năng kiểm thử cao hơn cho các nhà phát triển và giảm bớt độ phức tạp đối với người mới sử dụng.

* **Khả năng mở rộng của HTTP**

    Tính năng header HTTP đã được giới thiệu từ HTTP/1.0, đã tạo điều kiện thuận lợi cho việc mở rộng và thử nghiệm giao thức. Các chức năng mới có thể dễ dàng được giới thiệu thông qua thỏa thuận đơn giản giữa client và máy chủ về ý nghĩa của một header mới.

* **Tính stateless nhưng không phải sessionless của HTTP**

    Trong khi HTTP được xem là stateless, không giữ liên kết giữa hai yêu cầu được thực hiện liên tiếp trên cùng một kết nối, điều này có thể tạo ra thách thức khi người dùng cố gắng tương tác mạch lạc với các trang cụ thể, như việc sử dụng giỏ hàng trên các trang thương mại điện tử. Mặc dù vậy, một giải pháp tinh tế là sử dụng cookie HTTP, nhờ vào khả năng mở rộng của header. Cookie HTTP có thể được tích hợp vào quy trình hoạt động, cho phép tạo ra các phiên trạng thái trên mỗi yêu cầu HTTP, từ đó chia sẻ cùng một ngữ cảnh hoặc trạng thái.

* **Kết nối của HTTP**

    HTTP sử dụng kết nối kiểm soát ở tầng  truyền tải, do đó về cơ bản nằm ngoài phạm vi của HTTP. Dù HTTP không yêu cầu giao thức truyền tải cơ bản phải dựa trên sự kết nối, vì chỉ yêu cầu nó đáng tin cậy hoặc không bị mất message (ít nhất là trình báo 1 lỗi). Trong số hai giao thức truyền tải phổ biến nhất trên Internet, TCP thì đáng tin cậy còn UDP thì không. HTTP do đó dựa vào tiêu chuẩn TCP vốn là connection-based (dựa trên sự kết nối).

    ![](/thuctap/img/http_connection.png)

    Trước khi 1 client và server có thể trao đổi 1 cặp yêu cầu – phản hồi HTTP, chúng phải thiết lập 1 kết nối TCP, 1 quá trình vốn yêu cầu 1 số vòng lặp. Hoạt động mặc định của HTTP/1.0 là mở 1 kết nối TCP riêng biệt cho từng cặp yêu cầu – phản hồi HTTP. Điều này làm nó kém hiệu quả hơn việc chia sẻ 1 kết nối TCP đơn lẻ khi nhiều yêu cầu được gửi liên tiếp.

    Để giảm thiểu lỗ hỏng này, HTTP/1.1 đã giới thiệu pipelining (nhưng được chứng minh là khá khó để thực hiện) và kết nối liên tục: kết nối TCP bên dưới có thể được kiểm soát 1 phần bằng cách sử dụng tiêu đề Connection. HTTP/2 đã tiến 1 bước xa hơn bằng cách ghép các thông báo qua 1 kết nối duy nhất, giúp giữ cho kết nối ổn định và hiệu quả hơn.

    HTTP/3 là phiên bản mới nhất của HTTP, được thiết kế để cải thiện hiệu suất và độ tin cậy so với các phiên bản trước (HTTP/1.1 và HTTP/2). HTTP/3 sử dụng QUIC thay vì TCP.

# END