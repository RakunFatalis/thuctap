# Cách hoạt động của HTTP

# Mục lục

- [Cách hoạt động của HTTP](#cách-hoạt-động-của-http)
- [Mục lục](#mục-lục)
- [I. Luồng xử lí hoạt động của HTTP.](#i-luồng-xử-lí-hoạt-động-của-http)
- [II. HTTP Messages](#ii-http-messages)
  - [1. HTTP Requests](#1-http-requests)
  - [2. HTTP Responses](#2-http-responses)
  - [3. HTTP/2 Frames](#3-http2-frames)
- [END](#end)

# I. Luồng xử lí hoạt động của HTTP.


HTTP là một giao thức yêu cầu-đáp ứng, nghĩa là mỗi khi một khách hàng (thường là trình duyệt web) gửi một yêu cầu, máy chủ sẽ phản hồi lại bằng một phản hồi tương ứng. Quy trình cơ bản của một chu kỳ yêu cầu-đáp ứng HTTP diễn ra như sau:

1. **Khách hàng gửi yêu cầu HTTP:**

    Khách hàng (thường là trình duyệt web) bắt đầu quá trình bằng cách gửi một yêu cầu HTTP đến máy chủ. Yêu cầu này bao gồm phương thức yêu cầu (GET, POST, PUT, DELETE, v.v.), URI (Uniform Resource Identifier - Định danh tài nguyên thống nhất, ví dụ: một URL), các tiêu đề yêu cầu và một thân yêu cầu tùy chọn.

2. **Máy chủ xử lý yêu cầu:**

    Máy chủ nhận yêu cầu và xử lý nó dựa trên phương thức và tài nguyên được yêu cầu. Điều này có thể bao gồm việc truy xuất dữ liệu từ cơ sở dữ liệu, thực thi các kịch bản phía máy chủ hoặc thực hiện các thao tác khác.

3. **Máy chủ gửi phản hồi HTTP:**

    Sau khi xử lý yêu cầu, máy chủ gửi phản hồi HTTP trở lại khách hàng. Phản hồi này bao gồm mã trạng thái (ví dụ: 200 OK, 404 Not Found), các tiêu đề phản hồi và một thân phản hồi tùy chọn chứa dữ liệu hoặc nội dung được yêu cầu.

4. **Khách hàng xử lý phản hồi:**

    Khách hàng nhận phản hồi từ máy chủ và xử lý nó tương ứng. Ví dụ, nếu phản hồi chứa một trang HTML, trình duyệt sẽ hiển thị và hiển thị trang đó. Nếu đó là một hình ảnh hoặc tệp phương tiện khác, trình duyệt sẽ hiển thị hoặc xử lý nó phù hợp.

# II. HTTP Messages

HTTP Messages là cách dữ liệu được trao đổi giữa máy chủ và khách hàng. Có hai loại thông điệp: yêu cầu (requests) được gửi bởi khách hàng để kích hoạt một hành động trên máy chủ và phản hồi (responses), là câu trả lời từ máy chủ.

Các yêu cầu và phản hồi HTTP có cấu trúc tương tự nhau và bao gồm:

* **Dòng bắt đầu (start-line)** mô tả yêu cầu được thực hiện, hoặc trạng thái của nó là thành công hay thất bại. Đây luôn là một dòng duy nhất.

* Một tập hợp các **tiêu đề(headers)** HTTP tùy chọn chỉ định yêu cầu, hoặc mô tả nội dung của thân thông điệp.

* Một dòng trống **(empty line)** chỉ ra rằng tất cả thông tin meta cho yêu cầu đã được gửi.

* Một thân **(body)** tùy chọn chứa dữ liệu liên quan đến yêu cầu (như nội dung của một form HTML), hoặc tài liệu liên quan đến phản hồi. Sự hiện diện của thân và kích thước của nó được chỉ định bởi dòng bắt đầu và các tiêu đề HTTP.

Start-line và headers HTTP của HTTP Messages được gọi chung là phần đầu (head) của yêu cầu, trong khi đó phần tải (payload) của nó được gọi là phần thân (body).

![](/thuctap/img/httpmsgstructure2.png)

## 1. HTTP Requests

HTTP Requests là các thông điệp được gửi bởi khách hàng để khởi động một hành động trên máy chủ. Dòng yêu cầu của chúng chứa ba thành phần:

**Request line**


* **Một phương thức HTTP (HTTP method)**:

    Là một động từ (như GET, PUT hoặc POST) hoặc một danh từ (như HEAD hoặc OPTIONS), mô tả hành động sẽ được thực hiện. Ví dụ, GET chỉ ra rằng một tài nguyên cần được lấy về hoặc POST có nghĩa là dữ liệu được đẩy lên máy chủ (tạo mới hoặc chỉnh sửa một tài nguyên, hoặc tạo một tài liệu tạm thời để gửi lại).

* **Mục tiêu của yêu cầu (request target)**
    
    Thường là một URL, hoặc đường dẫn tuyệt đối của giao thức, cổng, và tên miền, thường được đặc trưng bởi ngữ cảnh của yêu cầu. Định dạng của mục tiêu yêu cầu này có thể khác nhau giữa các phương thức HTTP khác nhau. Nó có thể là:

    * **Một đường dẫn(path**), thường được theo sau bởi dấu '?' và chuỗi truy vấn. Đây là dạng phổ biến nhất, được gọi là dạng gốc (origin form), và được sử dụng với các phương thức GET, POST, HEAD và OPTIONS. Ví dụ:

      * ``POST / HTTP/1.1``
      * ``GET /background.png HTTP/1.0``
      * ``HEAD /test.html?query=alibaba HTTP/1.1``
      * ``OPTIONS /anypage.html HTTP/1.0``

    * **Một URL hoàn chỉnh**, được gọi là dạng tuyệt đối (absolute form), chủ yếu được sử dụng với phương thức GET khi kết nối với một máy chủ proxy. Ví dụ:

        ``GET https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1``

    * **Thành phần authority của một URL**, bao gồm tên miền và tùy chọn cổng (được thêm dấu ':'), được gọi là dạng authority. Nó chỉ được sử dụng với phương thức CONNECT khi thiết lập một đường hầm HTTP. Ví dụ:

        ``CONNECT developer.mozilla.org:80 HTTP/1.1``

    * **Dạng dấu sao (asterisk form)**, một dấu sao đơn ('*'), được sử dụng với phương thức OPTIONS để đại diện cho toàn bộ máy chủ. Ví dụ:

        ``OPTIONS * HTTP/1.1``

* **Phiên bản HTTP**

    Xác định cấu trúc của thông điệp còn lại, hoạt động như một chỉ thị về phiên bản dự kiến sẽ được sử dụng cho phản hồi.

**Headers**

HTTP headers từ một yêu cầu tuân theo cấu trúc cơ bản của một HTTP header: một chuỗi không phân biệt chữ hoa chữ thường, theo sau là dấu hai chấm (``':'``) và một giá trị có cấu trúc phụ thuộc vào header. Toàn bộ header, bao gồm cả giá trị, bao gồm một dòng duy nhất, có thể khá dài.

Nhiều loại tiêu đề khác nhau có thể xuất hiện trong các yêu cầu HTTP. Chúng có thể được chia thành các nhóm sau:

* **Tiêu đề chung (General headers)**: Như Via, áp dụng cho toàn bộ thông điệp.

* **Tiêu đề yêu cầu (Request headers)**: Như User-Agent hoặc Accept, điều chỉnh yêu cầu bằng cách chỉ định thêm thông tin (như Accept-Language), cung cấp ngữ cảnh (như Referer), hoặc hạn chế có điều kiện (như If-None-Match).

* **Tiêu đề biểu diễn (Representation headers)**: Như Content-Type, mô tả định dạng gốc của dữ liệu thông điệp và bất kỳ mã hóa nào đã được áp dụng (chỉ xuất hiện nếu thông điệp có phần thân).

![](/thuctap/img/header_http_request.png)

**Body**

Phần cuối cùng của HTTP Requests là body của nó. Không phải tất cả các yêu cầu đều có phần thân: các yêu cầu lấy tài nguyên như GET hoặc HEAD thường không cần một phần thân. Các yêu cầu gửi dữ liệu tới máy chủ để tạo ra một tài nguyên, chẳng hạn như yêu cầu PUT hoặc POST, thường yêu cầu một phần thân chứa dữ liệu được sử dụng để thực hiện yêu cầu (ví dụ: dữ liệu của một form HTML).

Các phần thân có thể được chia thành hai loại chính:

* **Thân đơn tài nguyên (Single-resource bodies)**: Bao gồm một tệp đơn, được xác định bởi hai tiêu đề: Content-Type và Content-Length.

* **Thân nhiều tài nguyên (Multiple-resource bodies)**: Bao gồm một thân đa phần (multipart), mỗi phần chứa một phần thông tin khác nhau. Điều này thường liên quan đến các form HTML.

## 2. HTTP Responses

**Status line**

Dòng bắt đầu của một HTTP Responses, gọi là dòng trạng thái (status line), chứa các thông tin sau:

* **Phiên bản giao thức (Protocol version)**: Thường là HTTP/1.1, nhưng cũng có thể là HTTP/1.0.

* **Mã trạng thái (Status code)**: Chỉ thị sự thành công hoặc thất bại của yêu cầu. Các mã trạng thái phổ biến bao gồm 200, 404, hoặc 302.

* **Văn bản trạng thái (Status text)**: Một mô tả ngắn gọn, chỉ mang tính thông tin, về mã trạng thái để giúp người dùng hiểu thông điệp HTTP.

Một dòng trạng thái điển hình trông như sau: ``HTTP/1.1 404 Not Found.``

**Headers**

HTTP headers trong phản hồi theo cùng một cấu trúc như bất kỳ header nào khác: một chuỗi không phân biệt chữ hoa chữ thường theo sau là dấu hai chấm (``':'``) và một giá trị có cấu trúc phụ thuộc vào loại tiêu đề. Toàn bộ tiêu đề, bao gồm cả giá trị của nó, xuất hiện trên một dòng duy nhất.

Nhiều loại header khác nhau có thể xuất hiện trong phản hồi. Chúng có thể được chia thành các nhóm sau:

* **Tiêu đề chung (General headers):** Như Via, áp dụng cho toàn bộ thông điệp.

* **Tiêu đề phản hồi (Response headers):** Như Vary và Accept-Ranges, cung cấp thông tin bổ sung về máy chủ mà không nằm trong dòng trạng thái.

* **Tiêu đề biểu diễn (Representation headers):** Như Content-Type, mô tả định dạng gốc của dữ liệu thông điệp và bất kỳ mã hóa nào đã được áp dụng (chỉ xuất hiện nếu thông điệp có phần thân).

![](/thuctap/img/header_http_responses.png)

**Body**

Phần cuối cùng của một phản hồi là body của nó. Không phải tất cả các phản hồi đều có phần body: các phản hồi với mã trạng thái đủ để trả lời yêu cầu mà không cần tải trọng tương ứng (như 201 Created hoặc 204 No Content) thường không có phần thân.

Các phần thân có thể được chia thành ba loại chính:

* **Thân đơn tài nguyên (Single-resource bodies)**: Bao gồm một tệp đơn với chiều dài đã biết, được xác định bởi hai tiêu đề: Content-Type và Content-Length.

* **Thân đơn tài nguyên (Single-resource bodies)**: Bao gồm một tệp đơn với chiều dài không xác định, được mã hóa theo từng khối với Transfer-Encoding được thiết lập là chunked.

* **Thân nhiều tài nguyên (Multiple-resource bodies)**: Bao gồm một thân đa phần (multipart), mỗi phần chứa một phần thông tin khác nhau. Những phần thân này khá hiếm.

## 3. HTTP/2 Frames

Các Messages HTTP/1.x có một số nhược điểm về hiệu suất:

* **Header không được nén**: Khác với phần body, header không được nén, dẫn đến việc tiêu tốn băng thông không cần thiết.

* **Header thường giống nhau từ messages này sang messages khác**: Mặc dù các eader thường giống nhau, chúng vẫn được lặp lại qua các kết nối, làm tăng kích thước dữ liệu được truyền tải.

* **HTTP/1.1 có hỗ trợ pipelining**: Tuy nhiên, tính năng này không được kích hoạt mặc định trong hầu hết các trình duyệt và không cho phép multiplexing (tức là gửi các yêu cầu đồng thời). Để gửi các yêu cầu đồng thời, cần phải mở nhiều kết nối đến cùng một máy chủ; và các kết nối TCP đã được giữ ấm (warm TCP connections) hiệu quả hơn các kết nối mới (cold connections).

HTTP/2 giới thiệu một bước bổ sung:

* **Chia thông điệp HTTP/1.x thành các khung (frames)**: Các khung được nhúng trong một luồng (stream). Các khung dữ liệu và tiêu đề được tách biệt, cho phép nén tiêu đề.

* **Đa luồng (Multiplexing)**: Nhiều luồng có thể được kết hợp lại, cho phép sử dụng hiệu quả hơn các kết nối TCP cơ bản.

![](/thuctap/img/http2.png)

Các khung HTTP (HTTP frames) hiện đã trở nên trong suốt đối với các nhà phát triển Web. Đây là một bước bổ sung trong HTTP/2, nằm giữa các thông điệp HTTP/1.1 và giao thức vận chuyển cơ bản. Các nhà phát triển Web không cần phải thay đổi các API mà họ sử dụng để tận dụng các khung HTTP; khi HTTP/2 có sẵn cả trong trình duyệt và máy chủ, nó sẽ được kích hoạt và sử dụng tự động.

# END