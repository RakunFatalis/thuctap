# WHAT IS WEB SERVER

# MỤC LỤC

- [WHAT IS WEB SERVER](#what-is-web-server)
- [MỤC LỤC](#mục-lục)
  - [I. Web Server là gì](#i-web-server-là-gì)
    - [1. Khái niệm](#1-khái-niệm)
    - [2. Thành phần chính của Web Server](#2-thành-phần-chính-của-web-server)
    - [3. Chức năng chính của Web Server](#3-chức-năng-chính-của-web-server)
    - [4. Triển khai Web Server](#4-triển-khai-web-server)
  - [II. Hiện nay có bao nhiêu loại Web Server?](#ii-hiện-nay-có-bao-nhiêu-loại-web-server)
  - [III. Cách thức hoạt động của Web Server](#iii-cách-thức-hoạt-động-của-web-server)
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

Hai phần chính quan trọng để thực hiện cấu hình Web Server không thể thiếu đó là phần cứng hoặc phần mềm, đôi khi phải cả phần mềm lẫn phần cứng.

* **Về mặt phần cứng :**

    Một web server là một máy tính lưu trữ các phần mềm và các tệp thành phần của web (như là, tệp HTML, hình ảnh, tệp CSS và file JavaScript). Web server kết nối Internet và hỗ trợ trao đổi dữ liệu với các thiết bị khác kết nối tới web

* **Về mặt phần mềm**

    Một web server bao gồm nhiều thành phần kiểm soát cách người dùng web truy cập vào các tệp được lưu trữ. Tối thiểu nó phải là một máy chủ dùng giao thức HTTP, một máy chủ HTTP là phần mềm hiểu các **URL** (địa chỉ web) và **HTTP** (giao thức mà trình duyệt của bạn sử dụng để xem các trang web).
    
    Một máy chủ HTTP có thể được truy cập thông qua các tên miền của các trang web mà nó lưu trữ, và nó cung cấp nội dung của các trang web được lưu trữ này đến thiết bị của người dùng cuối.

Về cơ bản, mỗi khi một trình duyệt cần một tệp được lưu trữ trên máy chủ, trình duyệt sẽ gửi yêu cầu tới giao thức HTTP. Khi yêu cầu được gửi đến đúng địa chỉ (**phần cứng**) của web server, máy chủ HTTP (**phần mềm**) sẽ chấp nhận yêu cầu và đi tìm tệp được yêu cầu và gửi lại cho trình duyệt cũng qua HTTP. **Nếu máy chủ không tìm thấy tài liệu được yêu cầu, nó sẽ trả về phản hồi 404.**

![](/img/Webserver_comp.png)


### 3. Chức năng chính của Web Server

Web server là một phần mềm hoặc thiết bị phần cứng chịu trách nhiệm xử lý yêu cầu từ trình duyệt web và trả về nội dung tương ứng cho người dùng qua mạng Internet. Sau đây mình sẽ liệt kê một số các chức năng mà mọi người nên biết

* **Lưu trữ và cung cấp nội dung web**

    * **Lưu trữ nội dung (Storing content)**: Web server lưu trữ các tệp cần thiết để hiển thị một trang web. Các tệp này bao gồm các trang web (HTML), hình ảnh, video, và các tệp khác như CSS và JavaScript. Các tệp này được lưu trữ trên các thiết bị lưu trữ của máy chủ, chẳng hạn như ổ cứng hoặc SSD.

    * **Cung cấp nội dung (Delivering content)****Cung cấp nội dung (Delivering content)**: Khi một khách hàng (thường là trình duyệt web) yêu cầu một trang web hoặc một tài nguyên cụ thể từ máy chủ, web server sẽ gửi lại nội dung đó cho khách hàng.

* **Xử lí các yêu cầu HTTP**

    Web server xử lý các yêu cầu HTTP từ các khách hàng hoặc người dùng. Giao thức HTTP là giao thức tiêu chuẩn được sử dụng để giao tiếp giữa các máy chủ web và khách hàng. Khi một khách hàng yêu cầu một trang web hoặc nội dung web khác, yêu cầu đó được gửi đến máy chủ web qua internet. Sau đó, máy chủ web sẽ xử lý yêu cầu, truy xuất nội dung được yêu cầu từ các thiết bị lưu trữ của nó, và gửi lại nội dung đó cho khách hàng dưới dạng một phản hồi HTTP.

* **Hỗ trợ chuyển đổi thông minh**

    Phần mềm web server cũng giống như các phần mềm khác, nó cho phép người dùng cài đặt và hoạt động trên bất kỳ máy tính nào đáp ứng đủ yêu cầu về bộ nhớ.

Vì thế khi thiết kế website xong, cần thực hiện đăng tải website lên web server để giúp khách hàng có thể truy cập web ở nhiều nơi trên thế giới và hiểu được nội dung bên trong. Một web server chất lượng sẽ giúp gia tăng hiệu quả hoạt động của website từ đó hỗ trợ người dùng truy cập thông tin dễ dàng, nhanh chóng.

### 4. Triển khai Web Server

Để triển khai một trang web, bạn cần có Web Server tĩnh (Static) và động (Dynamic)

  * **Static Web Server:** bao gồm một máy tính (phần cứng) với một máy chủ HTTP (phần mềm). Chúng ta gọi nó là "tĩnh" vì máy chủ gửi các tập tin lưu trữ của nó đúng như vậy đến trình duyệt của bạn.
  * **Dynamic Web Server:** Gồm Server tĩnh và các phần mềm mở rộng khác, có thể là Databases, Application Server.

Ví dụ, để tạo ra các trang web mà bạn thấy trong trình duyệt, máy chủ có thể điền một mẫu HTML với nội dung từ cơ sở dữ liệu. Các trang web như MDN hoặc Wikipedia có hàng nghìn trang web. Thông thường, các trang web kiểu này được cấu thành từ chỉ một vài mẫu HTML và một cơ sở dữ liệu khổng lồ, thay vì hàng nghìn tài liệu HTML tĩnh. Cấu hình này giúp dễ dàng hơn trong việc bảo trì và cung cấp nội dung.

## II. Hiện nay có bao nhiêu loại Web Server?

Các web server có nhiều loại khác nhau, mỗi loại được thiết kế để đáp ứng các yêu cầu cụ thể và phục vụ các khối lượng công việc khác nhau. Hiểu rõ các loại web server khác nhau là rất quan trọng để chọn lựa tùy chọn phù hợp nhất dựa trên các yếu tố như hiệu suất, khả năng mở rộng, bảo mật và tương thích với các ứng dụng web. Dưới đây là một số loại web server.

* **Apache Web Server:**


    Apache là một trong những web server được sử dụng nhiều nhất nhờ vào sự đa dạng và linh hoạt của nó. Nó tương thích với nhiều hệ điều hành, do đó có thể được sử dụng bởi một lượng lớn khách hàng. Cách tiếp cận mô-đun tinh vi cũng cung cấp sự tự do cấu hình đáng kể, cho phép người dùng thêm hoặc loại bỏ các tùy chọn chức năng theo nhu cầu. Apache rất linh hoạt trong việc xử lý các loại yêu cầu, từ nội dung tĩnh đến nội dung động. Đã có một sự tiếp nhận lớn đối với ứng dụng này và do đó nó có một cộng đồng lớn và nhiều tài liệu hỗ trợ, làm cho việc hỗ trợ và khắc phục sự cố trở nên dễ dàng hơn.

* **Nginx Web Servers**

    Nginx nổi bật vì tính nhanh chóng, hiệu quả trong việc sử dụng tài nguyên hệ thống và khả năng xử lý khối lượng lớn lưu lượng truy cập. Nó nổi bật trong việc quản lý nhiều kết nối, một yếu tố làm cho nó được ưa chuộng cho các trang web quy mô lớn. Hơn nữa, Nginx thường được sử dụng như một máy chủ proxy HTTP ngược (reverse proxy), bộ cân bằng tải (load balancer) và bộ nhớ đệm HTTP (HTTP cache), ...

    Vì Nginx là một hệ thống dựa trên sự kiện (event-driven), nó có khả năng xử lý hàng nghìn kết nối cùng lúc mà không gặp phải vấn đề lớn. Nhờ vào đặc điểm này, các cài đặt phần mềm phức tạp hơn không làm tốn tài nguyên hệ thống của nó, giúp tăng tốc độ phản hồi. Điều này làm cho Nginx trở thành giải pháp được nhiều ứng dụng và dịch vụ web quy mô lớn yêu thích sử dụng.

* **IIS Web Servers**

    Được Microsoft thiết lập, IIS (Internet Information Services) khá tương thích với các sản phẩm và giải pháp Microsoft liên quan khác. Nó được khen ngợi vì dễ sử dụng và bảo mật cao, đặc biệt trong các bối cảnh liên quan đến Windows. IIS đặc biệt phù hợp với các ứng dụng web và trang web được phát triển bằng các công cụ của bộ công cụ Microsoft. Máy chủ này hỗ trợ hầu hết các giao thức và tiêu chuẩn để tương thích với nhiều giải pháp web khác nhau. Nó có các tính năng quản lý mạnh mẽ, giúp việc quản trị và giám sát trở nên khá dễ dàng. Các phát triển hiện tại của IIS được thực hiện cho Windows Server nhằm làm cho nó hiệu quả và đáng tin cậy hơn cho việc sử dụng ứng dụng quy mô lớn.

* **LiteSpeed Web Servers**

    LiteSpeed cũng không tiêu tốn tài nguyên quá mức; nó đặc biệt nổi bật về hiệu suất cao. Các tính năng như đặt bộ nhớ đệm và bảo mật nâng cao là những điểm mạnh của gói hosting web cho doanh nghiệp nhỏ. Dựa trên thực tế rằng LiteSpeed là hệ thống dựa trên sự kiện (event-driven), nó tối ưu cho các ứng dụng động và yêu cầu cao, bao gồm lưu lượng truy cập lớn trên web. Vì nó có khả năng xử lý nhiều kết nối đồng thời, nên rất phù hợp với các trang web nhận được nhiều kết nối.

    Việc chuyển đổi giữa LiteSpeed và Apache là khá dễ dàng vì không cần phải thiết kế lại máy chủ một cách phức tạp để tương thích với Apache. Các tùy chọn khác nhau của LiteSpeed giúp tăng tốc thời gian tải trang web, từ đó cải thiện trải nghiệm của người dùng.

* **Apache Tomcat**

    Apache Tomcat là phần mềm máy chủ web đa nền tảng, chứa Servlet và JavaServer Pages (JSP), được phát triển và phân phối bởi Apache Software Foundation cho các ứng dụng dựa trên Java. Nó cũng có khả năng cung cấp môi trường thực thi ổn định và hiệu quả cho các ứng dụng Java Servlet, JavaServer Pages (JSP) và Java Expression Language (EL). Tomcat, với tư cách là một ứng dụng web Java, dễ cấu hình và triển khai, do đó trở thành lựa chọn của nhiều nhà phát triển Java.

    Tài liệu chi tiết và sự hỗ trợ mạnh mẽ từ cộng đồng có nghĩa là các vấn đề của nó được ghi lại và giải quyết, hoặc mọi người học hỏi từ các sai lầm của mình. Nhờ vào độ tin cậy cao và khả năng mở rộng của máy chủ, nó rất phù hợp cho các ứng dụng doanh nghiệp quy mô lớn. Phần nào, sự tích hợp này sử dụng kết nối với các công nghệ Java khác để đảm bảo rằng Tomcat tuân thủ các môi trường dựa trên Java.

* **Node. js**

    Node.js là một môi trường runtime cho phép JavaScript chạy trên phía máy chủ. Nó nổi tiếng với mô hình hệ thống dựa trên sự kiện, có nghĩa là nó hỗ trợ các hoạt động không chặn (non-blocking) từ phía người gọi. Điều này làm cho Node.js đặc biệt lý tưởng cho các ứng dụng nhạy cảm về thời gian như máy chủ trò chuyện, trò chơi và các luồng trực tiếp. Điều này là do nền tảng có tính khả dụng cao và khả năng mở rộng, vì nó có thể xử lý nhiều kết nối đồng thời cùng một lúc.

    Ngoài ra, Node.js được triển khai thông qua các trình quản lý gói như npm (Node Package Manager) có một thư viện rộng lớn gồm các công cụ và thư viện. Nhờ vào sự nhẹ nhàng và khả năng thực thi nhanh, Node.js có thể được xem là một công cụ hoàn hảo cho các ứng dụng web hiện đại.

## III. Cách thức hoạt động của Web Server

Trong mô hình client-server, máy chủ web và máy chủ ứng dụng tương tác và làm việc với nhau. Client (khách hàng) là thực thể yêu cầu truy cập vào một trang web, trong khi server (máy chủ) cung cấp trang web đó. Quá trình này sử dụng giao thức HTTP để phản hồi các yêu cầu được thực hiện qua World Wide Web. Giao thức này cho phép các máy tính trao đổi thông tin bằng trình duyệt web của họ.

![](/img/Web_Servers_work.png)

Toàn bộ quá trình hoạt động của máy chủ web có thể được chia thành các bước sau:

* **Yêu cầu và địa chỉ**

    Quá trình bắt đầu khi bạn gõ một URL vào trình duyệt web của mình. Trình duyệt xử lý thông tin nhập vào để tìm vị trí vật lý của máy chủ web chứa các tệp liên quan. Do đó, bước đầu tiên liên quan đến việc yêu cầu một trang web và sử dụng trình duyệt để tra cứu địa chỉ của nó.

* **Chi tiết tìm kiếm của trình duyệt web**

    Việc tìm kiếm máy chủ web yêu cầu bắt đầu bằng việc chuyển đổi địa chỉ web thành một địa chỉ IP sử dụng Hệ thống Tên Miền (DNS). Vì địa chỉ IP là một số duy nhất được gán cho mỗi thiết bị trên Internet, việc xác định địa chỉ IP giúp nhận diện các máy chủ ứng dụng mà yêu cầu phải được gửi đến.

* **Yêu cầu nhận tại phần mềm máy chủ web**

    Trình duyệt web sử dụng một máy chủ HTTP để yêu cầu truy cập vào phần mềm máy chủ web liên quan. Yêu cầu nhận được tại máy chủ web nguồn chứa thông tin về trang web cụ thể cần được truy cập.

* **Tìm kiếm các tệp được yêu cầu**

    Phần mềm máy chủ web tìm kiếm các tệp được lưu trữ ở phía nó để tìm các tệp được yêu cầu. Những tệp này có thể là các tài liệu HTML, hình ảnh cho đến các chương trình tạo ra nội dung web động.

* **Phản hồi yêu cầu**

    Khi quá trình tìm kiếm của phần mềm máy chủ hoàn tất, thông tin được truyền lại cho trình duyệt sử dụng một máy chủ HTTP. Trình duyệt web của bạn sẽ hiển thị kết quả liên quan nếu các tệp được tìm thấy bởi máy chủ.

    Nếu không tìm thấy các tệp, trình duyệt sẽ hiển thị thông báo lỗi 404 Not Found. Ngoài ra, lỗi 403 cũng có thể được hiển thị nếu có vấn đề về quyền truy cập.


Vì vậy, quá trình trên được thực hiện mỗi khi bạn gõ một URL vào trình duyệt web để lấy thông tin liên quan từ nguồn web. Các máy chủ HTTP là những người đưa tin được chỉ định để lấy thông tin yêu cầu từ phía cuối cùng đến giao diện phía trước để hiển thị.
# END