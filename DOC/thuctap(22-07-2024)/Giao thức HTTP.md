# HTTP

# Mục lục

- [HTTP](#http)
- [Mục lục](#mục-lục)
  - [I. Giao thức HTTP là gì?](#i-giao-thức-http-là-gì)
  - [II. Các thành phần của HTTP](#ii-các-thành-phần-của-http)
    - [1. Client: the user-agent](#1-client-the-user-agent)
    - [2. The Web server](#2-the-web-server)
    - [3. Proxies](#3-proxies)
  - [III. Các tính năng có thể được kiểm soát bởi HTTP](#iii-các-tính-năng-có-thể-được-kiểm-soát-bởi-http)
  - [IV. Luồng xử lí của HTTP](#iv-luồng-xử-lí-của-http)
  - [V. HTTP Messages](#v-http-messages)
    - [HTTP Request](#http-request)
    - [HTTP Response](#http-response)



## I. Giao thức HTTP là gì?

HTTP là một giao thức để truy xuất các tài nguyên như tài liệu HTML thông qua internet. Nó là nền tảng của bất kỳ sự trao đổi dữ liệu nào trên Web và là một giao thức client-server, có nghĩa là các yêu cầu được khởi tạo bởi người nhận, thường là trình duyệt Web. Một tài liệu hoàn chỉnh thường được xây dựng từ các tài nguyên như nội dung văn bản, hướng dẫn bố cục, hình ảnh, video, tập lệnh, và nhiều thứ khác.

![](/img/http.png)

Các máy khách và máy chủ giao tiếp bằng cách trao đổi các thông điệp riêng lẻ (trái ngược với một luồng dữ liệu liên tục). Các thông điệp được gửi bởi máy khách được gọi là yêu cầu (requests) và các thông điệp được gửi bởi máy chủ để trả lời được gọi là phản hồi (responses).

## II. Các thành phần của HTTP

HTTP là một giao thức **client-server**: các yêu cầu được gửi bởi một thực thể, gọi là user-agent (hoặc một proxy). Hầu hết thời gian, user-agent là một trình duyệt web, nhưng nó có thể là bất kỳ thứ gì, ví dụ, một robot mà thu thập và duy trì chỉ mục của công cụ tìm kiếm.

Mỗi yêu cầu riêng lẻ được gửi đến một máy chủ, máy chủ sẽ xử lý nó và cung cấp một câu trả lời gọi là phản hồi. Giữa client và máy chủ có nhiều thực thể, được gọi chung là proxy, thực hiện các hoạt động khác nhau và đóng vai trò là cổng hoặc bộ nhớ đệm, chẳng hạn như.

![](/img/http_components.png)

### 1. Client: the user-agent

**User-agent** là bất kỳ công cụ nào hoạt động thay mặt cho người dùng. Vai trò này chủ yếu được thực hiện bởi trình duyệt web, nhưng nó cũng có thể được thực hiện bởi các chương trình mà kỹ sư và nhà phát triển web sử dụng để gỡ lỗi ứng dụng của họ.

Trình duyệt luôn là thực thể khởi tạo yêu cầu. Nó không bao giờ là máy chủ (mặc dù một số cơ chế đã được thêm vào qua các năm để mô phỏng các thông điệp khởi tạo từ máy chủ).

Để hiển thị một trang web, trình duyệt gửi một yêu cầu ban đầu để lấy tài liệu HTML đại diện cho trang. Sau đó, nó phân tích tệp này, tạo thêm các yêu cầu tương ứng với các script thực thi, thông tin bố cục (CSS) để hiển thị, và các tài nguyên phụ trong trang (thường là hình ảnh và video). Trình duyệt web sau đó kết hợp các tài nguyên này để trình bày tài liệu hoàn chỉnh, trang web. Các script thực thi bởi trình duyệt có thể lấy thêm tài nguyên ở các giai đoạn sau và trình duyệt cập nhật trang web tương ứng.

Một trang web là một tài liệu siêu văn bản. Điều này có nghĩa là một số phần của nội dung hiển thị là các liên kết, có thể được kích hoạt (thường bằng cách nhấp chuột) để lấy một trang web mới, cho phép người dùng điều hướng user-agent của họ và duyệt web. Trình duyệt dịch các hướng dẫn này thành các yêu cầu HTTP và tiếp tục diễn giải các phản hồi HTTP để trình bày cho người dùng một phản hồi rõ ràng.

### 2. The Web server

Ở phía đối diện của kênh giao tiếp là máy chủ, cung cấp tài liệu theo yêu cầu của khách hàng. Một máy chủ xuất hiện như chỉ là một máy duy nhất về mặt ảo; nhưng nó có thể thực sự là một tập hợp các máy chủ chia sẻ tải (cân bằng tải), hoặc một phần mềm phức tạp truy vấn các máy tính khác (như bộ nhớ đệm, máy chủ cơ sở dữ liệu, hoặc máy chủ thương mại điện tử), tạo ra tài liệu theo yêu cầu một cách hoàn toàn hoặc một phần.

Một máy chủ không nhất thiết phải là một máy duy nhất, mà nhiều phiên bản phần mềm máy chủ có thể được lưu trữ trên cùng một máy. Với HTTP/1.1 và tiêu đề Host, chúng thậm chí có thể chia sẻ cùng một địa chỉ IP.

### 3. Proxies

Giữa trình duyệt web và máy chủ, nhiều máy tính và thiết bị chuyển tiếp các thông điệp HTTP. Do cấu trúc phân lớp của ngăn xếp Web, hầu hết trong số này hoạt động ở các lớp vận chuyển, mạng hoặc vật lý, trở nên trong suốt ở lớp HTTP và có thể có tác động đáng kể đến hiệu suất. Những thiết bị hoạt động ở các lớp ứng dụng thường được gọi là **proxy**. Các proxy này có thể trong suốt, chuyển tiếp các yêu cầu mà chúng nhận được mà không thay đổi chúng theo bất kỳ cách nào, hoặc không trong suốt, trong trường hợp này chúng sẽ thay đổi yêu cầu theo một cách nào đó trước khi chuyển tiếp đến máy chủ. Proxy có thể thực hiện nhiều chức năng:


* **Bộ nhớ đệm (Caching)**: Cache có thể công cộng hoặc riêng tư, như bộ nhớ đệm của trình duyệt.

* **Lọc (Filtering)**: Như quét virus hoặc kiểm soát của cha mẹ.

* **Cân bằng tải (Load balancing)**: để cho phép nhiều máy chủ phục vụ các yêu cầu khác nhau.

* **Xác thực (Authentication)**: Để kiểm soát truy cập vào các tài nguyên khác nhau.

* **Ghi log (Logging)**: cho phép lưu trữ thông tin lịch sử.

## III. Các tính năng có thể được kiểm soát bởi HTTP

Tính mở rộng của HTTP đã và đang cho phép kiểm soát và chức năng nhiều hơn cho Web. Các phương pháp bộ nhớ đệm (cache) và xác thực là những chức năng được xử lý từ những ngày đầu của lịch sử HTTP. Khả năng nới lỏng ràng buộc nguồn gốc, ngược lại, chỉ được thêm vào trong những năm 2010.

Dưới đây là danh sách các tính năng phổ biến có thể được kiểm soát bằng HTTP:

* **Bộ nhớ đệm (Caching)**:

    Cách tài liệu được lưu vào bộ nhớ đệm có thể được kiểm soát bởi HTTP. Máy chủ có thể chỉ định cho các proxy và client về những gì nên được nhớ vào bộ nhớ đệm và trong bao lâu. Client có thể yêu cầu các cache proxy trung gian bỏ qua tài liệu đã lưu trữ.

* **Nới lỏng ràng buộc nguồn gốc (Relaxing the origin constraint)**: 

    Để ngăn chặn việc dò xét và xâm phạm quyền riêng tư, các trình duyệt web thực thi sự phân cách nghiêm ngặt giữa các trang web. Chỉ có các trang từ **cùng một nguồn gốc** mới có thể truy cập tất cả thông tin của một trang web. Mặc dù ràng buộc này sẽ gây khó khăn cho máy chủ, các headers HTTP có thể nới lỏng sự phân cách nghiêm ngặt này ở phía máy chủ, cho phép một tài liệu trở thành một mảnh ghép của thông tin được lấy từ các miền khác nhau; thậm chí có thể có lý do liên quan đến bảo mật để làm điều này.

* **Xác thực (Authentication)**:

    Một số trang có thể được bảo vệ để chỉ những người dùng cụ thể mới có thể truy cập chúng. Xác thực cơ bản có thể được cung cấp bởi HTTP, bằng cách sử dụng các tiêu đề như WWW-Authenticate, hoặc bằng cách thiết lập một phiên cụ thể sử dụng cookie HTTP.

* **Proxy và tunneling**:

    Máy chủ hoặc client thường nằm trên các hệ thống mạng riêng và ẩn địa chỉ IP thực của chúng khỏi các máy tính khác. Các yêu cầu HTTP sau đó đi qua các proxy để vượt qua rào cản này. Không phải tất cả các proxy đều là proxy HTTP. Ví dụ, giao thức SOCKS hoạt động ở cấp độ thấp hơn. Các giao thức khác, như ftp, có thể được xử lý bởi các proxy này.

* **Phiên làm việc (Sessions)**:

    Sử dụng cookie HTTP cho phép bạn liên kết các yêu cầu với trạng thái của máy chủ. Điều này tạo ra các phiên làm việc, mặc dù HTTP cơ bản là một giao thức stateless. Điều này hữu ích không chỉ cho giỏ hàng thương mại điện tử, mà còn cho bất kỳ trang web nào cho phép người dùng cấu hình đầu ra.

## IV. Luồng xử lí của HTTP

Khi một client muốn giao tiếp với một server, hoặc là server cuối cùng hoặc là một proxy trung gian, nó thực hiện các bước sau:

* **Mở kết nối TCP**:

    Kết nối TCP là một kênh liên lạc giữa client và server, cho phép gửi và nhận dữ liệu. Client có thể mở kết nối mới mỗi khi cần gửi yêu cầu, hoặc tái sử dụng kết nối hiện có để gửi nhiều yêu cầu và nhận nhiều phản hồi mà không phải thiết lập kết nối mới mỗi lần.

* **Gửi thông điệp HTTP**:

  * **HTTP trước HTTP/2**: Các thông điệp HTTP trước phiên bản HTTP/2 là dạng văn bản thuần túy (plain text) và có thể đọc được dễ dàng, ví dụ như yêu cầu GET hoặc POST.

  * **HTTP/2**: Trong HTTP/2, các thông điệp HTTP không còn là văn bản thuần túy mà được đóng gói trong các khung (frames). Điều này giúp cải thiện hiệu suất và cho phép nhiều yêu cầu được gửi đồng thời qua một kết nối TCP duy nhất.

* **Đọc phản hồi gửi từ server:**

    Sau khi gửi yêu cầu, client sẽ nhận và đọc phản hồi từ server, chứa thông tin như mã trạng thái (200 OK, 404 Not Found) và nội dung dữ liệu.

* **Đóng hoặc tái sử dụng kết nối:**

    Sau khi giao dịch hoàn tất, kết nối có thể được đóng hoặc giữ mở để sử dụng cho các yêu cầu tiếp theo.

Nếu HTTP pipelining được kích hoạt, nhiều yêu cầu có thể được gửi mà không cần đợi phản hồi đầu tiên được nhận hoàn toàn. HTTP pipelining đã chứng tỏ là khó thực hiện trong các mạng hiện có, nơi phần mềm cũ đồng thời tồn tại với các phiên bản hiện đại. HTTP pipelining đã được thay thế trong HTTP/2 bằng cách đa luồng yêu cầu trong một khung (frame) để mạnh mẽ hơn.

## V. HTTP Messages

Các yêu cầu được tạo bởi client gửi tới web server và khi các web server gửi lại dữ liệu được gọi lần lượt là HTTP request và HTTP response. Chúng đều được gọi là HTTP message, là các message có cấu trúc đơn giản.

HTTP Message rất đơn giản, ta hoàn toàn có thể đọc được mà không nhất thiết phải có công cụ phân tích riêng biệt, nó làm giảm đi sự phức tạp khi phát triển hay khi debug ứng dụng.

* **Cấu trúc chung**

![](/img/http_same.png)

  * **Dòng đầu tiên (một dòng)**: Cho biết thông tin yêu cầu hoặc trạng thái (thành công hay lỗi) của response.
  
  * **Phần header (các dòng sau dòng đầu tiên trước một dòng trắng)**: Nó là một tập hợp các dòng chứa thông tin về HTTP Message, thông tin về phần body 

  * **Một dòng trắng cho biết phần thông tin (dòng đầu và header) đã gửi hết**
    
    Phần body chứa dữ liệu đính kèm với request (như HTML Form) hoặc nội dung văn bản đính kèm cùng response. Kích cỡ dữ liệu này (size) có được xác định bởi thông tin trong header.

Mặc dù có cấu trúc chung nhưng về chi chi tiết Request và Response có những đặc điểm riêng.

### HTTP Request

Http Request tập hợp thông tin được gửi từ các máy khách (client) đến máy chủ (server). Nó là những yêu cầu cần máy chủ tìm kiếm hoặc xử lý và phản hồi kết quả lại client. Các yêu cầu HTTP được gửi đến có thể là các file dưới dạng XML hoặc Json.

![](/img/http_request.png)


* **Request line**
    
    Đây là dòng đầu tiên của HTTP Request, với ba loại chính là method, path ( hay URL) và HTTP version. Cụ thể:

    * **Method**: gồm nhiều loại nhưng phổ biến nhất là GET và POST. Trong đó, phương thức GET có tác dụng dùng để yêu cầu các tài nguyên cung cấp trong URL.

    * **Path (URL)**: có tác dụng định danh các nguồn tài nguyên được yêu cầu bởi khách hàng, người dùng và bắt buộc phải có dấu “/".

    * **HTTP version**: Đây là phiên bản HTTP được sử dụng, trong đó phổ biến nhất là HTTP/1.0 hay HTTP/1.1. (Với các bản cập nhật gần đây của các trình duyệt như Chrome, giao thức được mặc định sử dụng nếu không có sự can thiệp của lập trình viên sẽ là HTTP/1.2 vì các giao thức đã kể hiện không còn đủ an toàn trước sự tấn công của các hacker)

* **Request Header**

    Yếu tố thứ hai góp phần làm hình thành HTTP Request đó là các header. Thông tin được bổ sung sẽ truyền tải giữa cả máy chủ và máy khách, chẳng hạn như cookie, thông tin về ủy quyền, tác nhân người dùng… Tương tự một HTTP Request, header sẽ phân biệt chữ thường và chữ hoa, theo sau đó là dấu “:” và một giá trị.

    ![](/img/http_request_header.png)

* **Message body**
    
    Yếu tố thứ ba được đề cập đến đó là Message body. Máy chủ dùng nội dung thư để cung cấp những thông thông tin cần thiết nhất đến với máy khách. Message body có chứa các dòng yêu cầu, thông tin, dòng trống, tiêu đề, và nội dung. Trong đó, yếu tố nội dung sẽ tùy chọn. Không phải tất cả các yêu cầu đều có nội dung nhưng sẽ dùng POST để phân phối tải trọng.

**Các phương thức để thực hiện một HTTP request**

* **GET**

    Get là một trong các phương thức được sử dụng nhiều nhất bởi phía Client. Nó cho phép Client gửi yêu cầu thông qua đường dẫn (URL) lên server. Web server sẽ nhận đường dẫn đó và phân tích để trả về kết quả cho bạn. 

    Phương thức GET không yêu cầu có request body để thực hiện. Khi bạn mở một trang web, client sẽ gửi lên server để truy xuất nội dung hiển thị của web, hành động này giống với một thao tác đọc của con người.

    Một số đặc điểm chính của phương thức Get là:

    * Giới hạn độ dài của các giá trị là 255 kí tự.
    
    * Chỉ hỗ trợ các dữ liệu kiểu String.
    
    * Có thể lưu vào bộ nhớ cache.
    
    * Các tham số truyền vào được lưu trữ trong lịch sử trình duyệt.
    
    * Có thể được bookmark (đánh dấu rồi xem lại sau) do được lưu trong lịch sử trình duyệt.

* **POST**

    Phương thức Post là phương thức gửi dữ liệu đến server giúp bạn có thể thêm mới dữ liệu hoặc cập nhật dữ liệu đã có vào database. Post cũng là một phương thức được sử dụng trong hầu hết các phiên làm việc sử dụng giao thức HTTP.

    Chúng ta sẽ gửi thông tin cần thêm hoặc cập nhật trong phần body request.

    Một số đặc điểm chính của Post là:

    * Dữ liệu cần thêm hoặc cập nhật không được hiển thị trong URL của trình duyệt.
    
    * Dữ liệu không được lưu trong lịch sử trình duyệt.
    
    * Không có hạn chế về độ dài của dữ liệu.
    
    * Hỗ trợ nhiều kiểu dữ liệu như: String, binary, integers,..

* **PUT**

    Cách hoạt động tương tự như Post nhưng nó chỉ được sử dụng để cập nhật dữ liệu đã có trong database. Khi sử dụng nó, bạn phải sửa toàn bộ dữ liệu của một đối tượng.

* **PATCH**

    Tượng tự như Post và Put, nhưng Patch được sử dụng khi phải cập nhật một phần dữ liệu của đối tượng.

* **DELETE**

    Giống như tên gọi, khi sử dụng phương thức Delete sẽ xóa các dữ liệu của server về tài nguyên thông qua URI. Cũng giống như GET, phương thức này không có body request.

* **HEAD**
    HEAD gần giống giống với lại GET, tuy nhiên nó không có response body.

    Nói một cách khác, nếu sử dụng phương thức GET tới đường dẫn /Books thì sẽ trả về danh sách các sản phẩm, còn khi sử dụng HEAD tới đường dẫn /Books nhưng không nhận được danh sách các sản phẩm.

    Truy vấn HEAD hữu ích khi chúng ta sử dụng nó để kiểm tra API có hoạt động không do không có response body nên thời gian phản hồi nhanh hơn so với phương thức Get. Và thường được sử dụng để kiểm tra trước khi download file do cứ gọi đến api dowload sẽ download file nên thêm phương thức head vào nó kiểm tra xem api có đang hoạt động tốt không tránh down nhiều.

### HTTP Response

HTTP Response được tạo ra bởi máy chủ gửi đến máy khách. Mục đích của phản hồi là cung cấp cho máy khách tài nguyên mà nó yêu cầu, hoặc thông báo cho máy khách rằng hành động mà nó yêu cầu đã được thực hiện; hoặc để thông báo cho máy khách rằng đã xảy ra lỗi trong quá trình xử lý yêu cầu của nó.

![](/img/http_responses.png)

* **Status Line (Dòng trạng thái):**

    Đây là dòng đầu tiên của HTTP Response, bao gồm ba phần chính là phiên bản HTTP, mã trạng thái và cụm từ giải thích. Cụ thể:

    * **HTTP Version**: Đây là phiên bản HTTP được sử dụng, ví dụ: HTTP/1.1.

    * **Status Code** (Mã trạng thái): Mã số chỉ trạng thái phản hồi của máy chủ, ví dụ: 200 (OK), 404 (Not Found), 500 (Internal Server Error).

    * **Status message** (Cụm từ giải thích): Cụm từ ngắn giải thích mã trạng thái, ví dụ: OK, Not Found, Internal Server Error.

* **Response Headers (Tiêu đề phản hồi)**:

    Các tiêu đề bổ sung thông tin về phản hồi như loại nội dung, kích thước nội dung, thông tin máy chủ, ngôn ngữ, v.v. Tương tự như trong yêu cầu HTTP, mỗi header sẽ có định dạng với một dấu hai chấm (:) và một giá trị.

* **Message Body (Thân phản hồi)**:

    Thân phản hồi chứa dữ liệu thực tế được trả về cho máy khách. Thân này có thể chứa HTML, JSON, XML hoặc bất kỳ dữ liệu nào khác tùy theo yêu cầu và không phải tất cả các phản hồi đều có thân phản hồi.

**Các status code của HTTP Response:**

Status Code là một số nguyên 3 ký tự, trong đó ký tự đầu tiên của mã hóa trạng thái định nghĩa hạng (loại) phản hồi và hai ký tự cuối không có bất cứ vai trò phân loại nào. Có 5 giá trị của ký tự đầu tiên như sau:

* **1xx (100 – 199): Information responses / Phản hồi thông tin**

Dưới đây là bảng liệt kê một số mã thường gặp

| Mã trạng thái | Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **100**| Continue| Máy chủ đã nhận được một phần của yêu cầu và máy khách nên tiếp tục gửi phần còn lại của yêu cầu.|
| **101**| Switching Protocols| Máy khách đã yêu cầu máy chủ chuyển đổi giao thức và máy chủ xác nhận rằng nó sẽ làm như vậy.|
| **102**| Processing| Máy chủ đã nhận được yêu cầu nhưng vẫn đang xử lý nó và chưa có phản hồi hoàn chỉnh.                      |
| **103**| Early Hints| Được sử dụng để trả về một số header phản hồi trước khi phản hồi HTTP thực sự hoàn chỉnh được gửi đến.    |

* **2xx (200 – 299): Successful responses / Phản hồi thành công**

Dưới đây là bảng liệt kê một số mã thường gặp

| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **200**| OK| Yêu cầu đã thành công và máy chủ đã trả về tài nguyên yêu cầu.       |
| **201**| Created| Yêu cầu đã thành công và một tài nguyên mới đã được tạo ra.          |
| **202**| Accepted| Yêu cầu đã được chấp nhận để xử lý, nhưng việc xử lý chưa hoàn tất.   |
| **204**| No Content| Yêu cầu đã thành công nhưng không có nội dung nào được trả về.       |
| **206**| Partial Content        | Máy chủ chỉ trả về một phần của tài nguyên do phạm vi tiêu đề được gửi bởi máy khách. |

* **3xx (300 – 399): Redirects / Điều hướng**

Dưới đây là bảng liệt kê một số mã thường gặp

| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **301**| Moved Permanently| Tài nguyên yêu cầu đã được di chuyển vĩnh viễn đến URL mới.|
| **302**| Found| Tài nguyên yêu cầu tạm thời được di chuyển đến URL mới.|
| **303**| See Other| Máy khách nên dùng GET để yêu cầu tài nguyên ở URL khác.|
| **304**| Not Modified| Tài nguyên không có sự thay đổi kể từ lần truy cập cuối.|
| **307**| Temporary Redirect| Tài nguyên yêu cầu tạm thời được di chuyển đến URL khác, nhưng phương thức HTTP không thay đổi. |
| **308**| Permanent Redirect| Tài nguyên yêu cầu đã được di chuyển vĩnh viễn đến URL mới và phương thức HTTP không thay đổi. |

* **4xx (400 – 499): Client errors / Lỗi phía client**

Dưới đây là bảng liệt kê một số mã thường gặp

| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **400**| Bad Request| Yêu cầu không hợp lệ hoặc máy chủ không thể hiểu yêu cầu.            |
| **401**| Unauthorized| Yêu cầu yêu cầu xác thực nhưng không được cung cấp hoặc không hợp lệ.|
| **403**| Forbidden| Máy chủ hiểu yêu cầu nhưng từ chối thực hiện nó.|
| **404**| Not Found| Máy chủ không thể tìm thấy tài nguyên yêu cầu.|
| **405**| Method Not Allowed| Phương thức yêu cầu không được phép trên tài nguyên yêu cầu.         |
| **408**| Request Timeout| Máy chủ không nhận được yêu cầu hoàn chỉnh từ máy khách trong thời gian cho phép. |
| **409**| Conflict| Yêu cầu không thể hoàn thành do xung đột với trạng thái hiện tại của tài nguyên. |
| **410**| Gone| Tài nguyên yêu cầu không còn tồn tại và không có địa chỉ chuyển hướng. |
| **429**| Too Many Requests| Máy khách đã gửi quá nhiều yêu cầu trong một khoảng thời gian ngắn.  |

* **5xx (500 – 599): Server errors / Lỗi phía máy chủ**

Dưới đây là bảng liệt kê một số mã thường gặp

| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **500**| Internal Server Error| Máy chủ gặp lỗi và không thể hoàn thành yêu cầu.|
| **501**| Not Implemented| Máy chủ không hỗ trợ chức năng cần thiết để hoàn thành yêu cầu.|
| **502**| Bad Gateway| Máy chủ hoạt động như một cổng hoặc proxy và nhận được phản hồi không hợp lệ từ máy chủ ngược lại. |
| **503**| Service Unavailable| Máy chủ hiện không thể xử lý yêu cầu do quá tải hoặc bảo trì.|
| **504**| Gateway Timeout| Máy chủ hoạt động như một cổng hoặc proxy và không nhận được phản hồi kịp thời từ máy chủ ngược lại. |
| **505**| HTTP Version Not Supported | Máy chủ không hỗ trợ phiên bản HTTP được sử dụng trong yêu cầu.|

#

