# Web Server hoạt động như thế nào.

# Mục lục


- [Web Server hoạt động như thế nào.](#web-server-hoạt-động-như-thế-nào)
- [Mục lục](#mục-lục)
  - [I. Cấu trúc và cơ chế hoạt động.](#i-cấu-trúc-và-cơ-chế-hoạt-động)
    - [1. Cấu trúc của Web Server](#1-cấu-trúc-của-web-server)
    - [2. Cơ chế hoạt động](#2-cơ-chế-hoạt-động)
  - [II. Cách thức lưu trữ file và giao tiếp thông qua HTTP trong web server](#ii-cách-thức-lưu-trữ-file-và-giao-tiếp-thông-qua-http-trong-web-server)
    - [1. Lưu trữ file](#1-lưu-trữ-file)
    - [2. Giao tiếp thông qua HTTP](#2-giao-tiếp-thông-qua-http)
- [END](#end)








## I. Cấu trúc và cơ chế hoạt động.

### 1. Cấu trúc của Web Server

Cấu trúc máy chủ web đề cập đến cấu trúc và thiết kế của các máy chủ web, mô tả cách chúng xử lý các yêu cầu đến và cung cấp nội dung web. Có hai cách tiếp cận chính trong kiến trúc máy chủ web:

* **Cấu trúc đơn tầng (Single-Tier - Máy chủ đơn):**

    Trong kiến trúc đơn tầng, một máy chủ duy nhất chịu trách nhiệm cả việc xử lý các yêu cầu và phục vụ nội dung web. Điều này phù hợp cho các trang web hoặc ứng dụng nhỏ với lưu lượng truy cập thấp. Tuy nhiên, nó có những hạn chế về khả năng mở rộng và khả năng dự phòng. Nếu máy chủ gặp sự cố, toàn bộ dịch vụ sẽ trở nên không khả dụng.

    ![](/thuctap/img/Single-Tier.png)

* **Kiến trúc đa tầng (Multi-Tier Architecture):**

    Trong kiến trúc đa tầng, nhiều máy chủ được sử dụng để phân phối khối lượng công việc và đảm bảo tính khả dụng cao. Phương pháp này thường liên quan đến các bộ cân bằng tải (load balancers) để phân phối đồng đều các yêu cầu đến một cụm máy chủ web. Mỗi máy chủ có thể phục vụ nội dung web độc lập, và nếu một máy chủ gặp sự cố, bộ cân bằng tải sẽ chuyển hướng lưu lượng truy cập đến các máy chủ còn lại, đảm bảo dịch vụ không bị gián đoạn.

    ![](/thuctap/img/multi-tier.png)


### 2. Cơ chế hoạt động

Khi bạn thực hiện truy cập vào một website ở môi trường internet, đồng nghĩa với việc bạn đang yêu cầu trang đó từ một web server. Ví dụ như bạn nhập đường link sau: https://google.com ở trình duyệt của mình. Lúc này web server sẽ nhận được yêu cầu từ trình duyệt của bạn và web server sẽ phản hồi lại trang. Dưới đây là 4 cách thức hoạt động của web server:

* **Trình duyệt web phân giải tên miền thành địa chỉ IP**

    Đầu tiên trình duyệt mà bạn đang dùng sẽ tiến hành xác định địa chỉ IP nào mà tên miền google.com trỏ về. Trong bộ nhớ cache không chứa sẵn thông tin này, thông qua internet trình duyệt gửi yêu cầu thông tin ở một hoặc có thể là nhiều máy chủ DNS. Máy chủ DNS thông báo cho trình duyệt biết địa chỉ IP nào mà tên miền sẽ trỏ đến.

* **Trình duyệt web yêu cầu URL đầy đủ**

    Khi trình duyệt web đã nhận ra địa chỉ IP của website, nó có thể yêu cầu URL đầy đủ ở web server.

* **Web server gửi phản hồi trang được yêu cầu**

    Web server phản hồi thông qua cách hồi đáp lại trang được yêu cầu. Trong trường hợp trang bị lỗi hoặc không còn tồn tại, webserver sẽ tiến hành phản hồi thông báo lỗi phù hợp.

* **Trình duyệt hiển thị trang web**

    Lúc này trình duyệt mà đang sử dụng sẽ nhận được trang và hiển thị trang theo yêu cầu trước đó. Khi phân tích về các vấn đề của trình duyệt web hay web server trong trường hợp này, bạn cũng có thể ngầm hiểu rằng: client (trình duyệt web) hay máy chủ (web server).

## II. Cách thức lưu trữ file và giao tiếp thông qua HTTP trong web server

### 1. Lưu trữ file

Đầu tiên, máy chủ sẽ phải lưu trữ các file của trang web đó bao gồm tất cả các file HTML và các file liên quan như css và javascript, fonts cùng những video …

Về mặt kỹ thuật thì bạn có thể thực hiên lưu trữ những file kể trên ở máy tính của mình, nhưng tốt nhất bạn nên lưu trữ dữ liệu đó vào các web server riêng có những đặc điểm như sau:

* Vận hành liên tục, ổn định.

* Đảm bảo kết nối internet ổn định.

* Cùng một địa chỉ IP. 

* Được hỗ trợ kỹ thuật từ một bên dịch vụ thứ 3. 

Từ những phân tích như trên thì việc tìm cho mình một nhà cung cấp hosting chất lượng, uy tín là vô cùng quan trọng trong việc phát triển website.

### 2. Giao tiếp thông qua HTTP

Tiếp theo là, một máy chủ cung cấp các dịch vụ hỗ trợ HTTP (Hypertext Transfer Protocol). HTTP có nhiệm vụ đưa ra phương thức truyền siêu văn bản giữa hai máy tính với nhau. Giao thức được định nghĩa là tập hợp gồm những quy tắt để truyền thông giữa hai máy tính với nhau. HTTP là giao thức nguyên bản, vô cấp.

* **Textual**: tất cả các lệnh là văn bản đơn thuần mà còn chúng ta có thể đọc.

* **Stateless**: Cả web server và trình duyệt web đều không ghi nhớ được những thao tác trước đó.

HTTP mang đến một cơ chế rất rõ ràng để người dùng và server có thể giao tiếp trao đổi dễ dàng với nhau. Dưới đây là những điều bạn cần lưu ý:

* Chỉ có khách và server và chỉ có server mới có quyền trao đổi request với nhau.

* Khi thực hiện yêu cầu một file bằng HTTP, khách phải cung cấp URL của file đó.

* Wed server phải trả lời mọi yêu cầu HTTP, ít nhất với thông báo lỗi.

Tại web server, máy chủ HTTP đảm nhiệm việc xử lý và trả lời những yêu cầu tới:

* Khi có yêu cầu, máy chủ HTTP phải xác nhận xem URL yêu cầu có tương thích với tệp đang có hay không.  

* Nếu có, máy chủ web sẽ gửi nội dung tệp tin đến trình duyệt. 

* Trong trường hợp là không, máy chủ ứng dụng thực hiện tạo tệp cần thiết. Hoặc không xử lý được, máy chủ web đưa tới thông báo lỗi cho trình duyệt, thông báo này sẽ là “404 Not Found”.

# END