# Web Server là gì

# MỤC LỤC
- [Web Server là gì](#web-server-là-gì)
- [MỤC LỤC](#mục-lục)
  - [I. Web Server là gì](#i-web-server-là-gì)
    - [1. Khái niệm](#1-khái-niệm)
    - [2. Thành phần chính của Web Server](#2-thành-phần-chính-của-web-server)
      - [a. Phần cứng (Hardware)](#a-phần-cứng-hardware)
      - [b. Phần mềm (Software)](#b-phần-mềm-software)
  - [II. Các loại Web Server phổ biến.](#ii-các-loại-web-server-phổ-biến)
- [END](#end)
## I. Web Server là gì

### 1. Khái niệm

Web server là một phần mềm hoặc phần cứng chịu trách nhiệm xử lý các yêu cầu từ khách hàng (client), thường là trình duyệt web, và cung cấp nội dung đáp ứng. Nội dung này có thể là trang web tĩnh (HTML, CSS, hình ảnh) hoặc trang web động được tạo ra bởi các ngôn ngữ lập trình phía máy chủ như PHP, Python, hoặc Node.js.

Web server truyền tải tài liệu đến khách hàng và bao gồm cả phần mềm và phần cứng. Web server có thể được sử dụng cục bộ (trong mạng công ty) hoặc chủ yếu qua Internet, từ đó cung cấp tài liệu cục bộ, trong công ty hoặc toàn cầu. 

![](/img/webserver.png)

Những chương trình trên web server được cài đặt nhằm phục vụ ứng dụng web. Khi được tiếp nhận các yêu cầu từ trình duyệt, webserver ngay lập tức sẽ gửi phản hồi đến client thông qua giao thức HTTP hoặc những giao thức khác.

Để làm được điều này, mỗi máy chủ web server phải là một kho có dung lượng rất lớn và có thể tải ở tốc độ rất cao để có thể lưu trữ và vận hành tốt mọi kho dữ liệu trên Internet. Thông qua các cổng giao tiếp riêng biệt, cấu hình máy chủ web được thiết lập giúp điều hành hiệu quả cho cả một hệ thống máy tính hoạt động trên Internet.

Xây dựng máy chủ web server phải đảm bảo được quy trình hoạt động khắc nghiệt, liên tục và không ngừng nghỉ để duy trì cung cấp dữ liệu thường xuyên cho mạng lưới máy tính. Tóm lại, đây sẽ là nơi chứa toàn bộ dữ liệu hoạt động trên internet mà nó được giao quyền quản lý. 


### 2. Thành phần chính của Web Server

Một web server là một hệ thống phức tạp bao gồm nhiều thành phần phần cứng và phần mềm khác nhau, kết hợp để cung cấp dịch vụ web cho người dùng. Dưới đây là các thành phần chính của một web server.

#### a. Phần cứng (Hardware)

* **Máy chủ vật lý (Physical Server):**

    Máy chủ vật lý là nền tảng cơ bản của web server, bao gồm các thành phần như CPU, RAM, ổ cứng, và các thiết bị mạng. Đây là nơi lưu trữ và xử lý tất cả các yêu cầu từ người dùng. Máy chủ vật lý thường được đặt trong các trung tâm dữ liệu với môi trường kiểm soát để đảm bảo hiệu suất và độ tin cậy cao.

* **Mạng (Network):**

    Hệ thống mạng kết nối các máy chủ với nhau và với người dùng. Bao gồm các thiết bị mạng như bộ định tuyến (router), bộ chuyển mạch (switch), và các kết nối internet tốc độ cao. Mạng giúp truyền tải dữ liệu giữa máy chủ và trình duyệt của người dùng.

#### b. Phần mềm (Software)

* **Hệ Điều Hành (Operating System)**

    Hệ điều hành là nền tảng quan trọng mà tất cả các phần mềm và dịch vụ của web server dựa vào. Nó quản lý tài nguyên phần cứng, cung cấp môi trường cho các ứng dụng chạy và đảm bảo tính ổn định và bảo mật của hệ thống.

* **HTTP Web Server**

    HTTP web server là chương trình chịu trách nhiệm xử lý các yêu cầu HTTP (Hypertext Transfer Protocol) từ các client (chủ yếu là các trình duyệt web) và cung cấp phản hồi dưới dạng các trang web, tài liệu, hoặc các tài nguyên khác.

* **Hệ Quản Trị Cơ Sở Dữ Liệu (Database Management System)**

    Hệ Quản Trị Cơ Sở Dữ Liệu (DBMS) là phần mềm giúp quản lý và tổ chức dữ liệu trong cơ sở dữ liệu. DBMS cung cấp các công cụ để tạo, đọc, cập nhật và xóa dữ liệu, đồng thời đảm bảo tính toàn vẹn, bảo mật và hiệu suất của dữ liệu.

* **Logging and Monitoring**
    
    Web servers thường có khả năng ghi log và giám sát để theo dõi và ghi lại các sự kiện quan trọng như yêu cầu của khách hàng, lỗi server và mức sử dụng tài nguyên. Những bản ghi này cung cấp cái nhìn quý giá để xử lý sự cố, phân tích và tối ưu hóa hiệu suất.

* **Security Mechanisms**
    
    Web servers thường triển khai các biện pháp bảo mật để bảo vệ server và dữ liệu đang được truyền tải. Điều này bao gồm các tính năng như mã hóa SSL/TLS để đảm bảo tính bảo mật và toàn vẹn của giao tiếp giữa server và khách hàng.

* **File System**
    
    Nơi lưu trữ nội dung web như các tệp HTML, hình ảnh, script và các tệp khác. Hệ thống tệp giúp server tìm và phục vụ các tệp yêu cầu từ khách hàng.

* **Configuration Files**
    
    Là các tập tin quan trọng dùng để quản lý và tùy chỉnh cách hoạt động của web server. Chúng xác định các cài đặt và chính sách mà web server sẽ tuân theo khi xử lý yêu cầu từ khách hàng.

Các thành phần này hoạt động cùng nhau để tạo nên các chức năng của web server. Web server động tạo ra và phục vụ nội dung động và tương tác với cơ sở dữ liệu hoặc các nguồn dữ liệu khác. Ngược lại, web server tĩnh bao gồm các tệp HTML đã có sẵn và phục vụ nội dung tĩnh yêu cầu mà không cần xử lý thêm. Cả hai loại server đều đóng góp vào việc nhận và xử lý các yêu cầu từ khách hàng. Chúng đảm bảo sự giao tiếp suôn sẻ giữa server và khách hàng bằng cách cung cấp nội dung yêu cầu một cách nhanh chóng.

## II. Các loại Web Server phổ biến.

* **Apache HTTP Server**

    ![](/thuctap/img/Apache_HTTP_server_logo_(2016).png)

    Apache HTTP Server, thường được gọi là Apache, là một chương trình dành cho máy chủ đối thoại qua giao thức HTTP. Apache chạy trên các hệ điều hành tương tự như Unix, Microsoft Windows, Novell Netware và các hệ điều hành khác. Apache đóng một vai trò quan trọng trong quá trình phát triển của mạng web thế giới 


    * **Khởi Đầu**: Apache bắt đầu như một dự án cộng đồng nhằm cải thiện và mở rộng NCSA HTTPd, một máy chủ web phổ biến vào cuối thập niên 1990. Sự phát triển này bắt đầu vào tháng 2 năm 1995.

    * **Apache Software Foundation**: Vào năm 1999, Apache Software Foundation (ASF) được thành lập để quản lý các dự án Apache, bao gồm Apache HTTP Server. ASF hiện tại quản lý nhiều dự án phần mềm mã nguồn mở khác ngoài Apache.

* **Nginx**

    ![](/thuctap/img/Nginx_logo.png)

    Nginx là một máy chủ web có thể được sử dụng như một reverse proxy, cân bằng tải, proxy email và bộ nhớ đệm HTTP. Phần mềm này được phát triển bởi nhà phát triển người Nga Igor Sysoev và được công khai phát hành vào năm 2004. Nginx là phần mềm mã nguồn mở, được cấp phép theo giấy phép BSD-2-Clause.

    Nginx có thể được cấu hình để phục vụ nội dung web tĩnh hoặc động như một máy chủ proxy.

    Nginx cũng có thể được triển khai để phục vụ nội dung động trên mạng bằng cách sử dụng các bộ xử lý FastCGI, SCGI cho các tập lệnh, các máy chủ ứng dụng WSGI hoặc các mô-đun Phusion Passenger, và có thể hoạt động như một cân bằng tải phần mềm.

    Nginx sử dụng phương pháp xử lý sự kiện bất đồng bộ, thay vì sử dụng các luồng, để xử lý các yêu cầu. Kiến trúc sự kiện module của Nginx có thể cung cấp hiệu suất dự đoán được dưới tải cao.

* **Microsoft IIS**

    ![](/thuctap/img/ISS.png)

    IIS là một máy chủ web có thể mở rộng được phát triển bởi Microsoft để sử dụng với dòng hệ điều hành Windows NT. IIS hỗ trợ các giao thức HTTP, HTTP/2, HTTP/3, HTTPS, FTP, FTPS, SMTP và NNTP.

    Nó đã trở thành một phần không thể thiếu của dòng hệ điều hành Windows NT kể từ Windows NT 4.0, mặc dù có thể không có sẵn trên một số phiên bản (ví dụ: phiên bản Windows XP Home) và không hoạt động theo mặc định.

    Phiên bản mới nhất của công cụ quản lý đi kèm với một bộ phần mềm chuyên dụng gọi là SEO Toolkit. Bộ công cụ này bao gồm nhiều công cụ cho SEO với các tính năng như tối ưu hóa thẻ meta / mã web, cấu hình sơ đồ trang web / robots.txt, phân tích website, thiết lập crawler, cấu hình SSL phía máy chủ và nhiều hơn nữa.

* **LiteSpeed**

    ![](/thuctap/img/litespeed.png)

    LiteSpeed hay LiteSpeed Web Server (được gọi tắt là LSWS) là một phần mềm máy chủ web độc quyền, có khả năng cung cấp hiệu suất nhanh và tiết kiệm tài nguyên mà không gây ảnh hưởng đến bảo mật của máy chủ. Đây là một máy chủ web được sử dụng rộng rãi bởi có thể mở rộng, bảo mật và cân bằng khi tải cao. Chống DDoS được tích hợp sẵn, cho phép kết nối trên mỗi IP và điều chỉnh băng thông.

**Tóm Tắt Mục Đích Sử Dụng:**

* Apache: Máy chủ web linh hoạt, phù hợp với nhiều loại cấu hình và môi trường khác nhau.

* Nginx: Máy chủ web hiệu suất cao và reverse proxy, tốt cho việc xử lý nhiều kết nối đồng thời và cân bằng tải.

* IIS: Máy chủ web dành riêng cho hệ điều hành Windows, tích hợp tốt với các công nghệ của Microsoft.

* LiteSpeed: Máy chủ web thương mại với hiệu suất cao, tối ưu hóa tốt cho nội dung động và các tính năng bảo mật nâng cao.

# END