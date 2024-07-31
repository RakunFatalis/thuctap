# Method và status code

# Mục lục
- [Method và status code](#method-và-status-code)
- [Mục lục](#mục-lục)
- [I. Method của HTTP](#i-method-của-http)
  - [1. HTTP Method Properties](#1-http-method-properties)
  - [2. 9 method của HTTP](#2-9-method-của-http)
- [II. Status code](#ii-status-code)
- [END](#end)


# I. Method của HTTP

## 1. HTTP Method Properties

Trong giao thức HTTP, các phương thức (methods) được thiết kế để thực hiện các hành động cụ thể trên các tài nguyên web. Mỗi phương thức có những tính chất riêng biệt giúp xác định cách chúng được sử dụng và tác động của chúng đến hệ thống. Các tính chất này bao gồm ``An toàn (Safe)``, ``Idempotent (Tính bất biến)``, ``Visibility (Tính che giấu thông tin)`` và ``Cacheable (Có thể cache được)``. 

* **An toàn (Safe)**

    Tính an toàn của một phương thức HTTP có nghĩa là phương thức đó không thay đổi trạng thái của server. Các phương thức an toàn chỉ nên được sử dụng để lấy thông tin mà không có bất kỳ tác động nào đến tài nguyên trên server.

* **Idempotent (Tính bất biến)**

    Một phương thức được gọi là idempotent nếu việc thực hiện nó nhiều lần có cùng một kết quả như thực hiện một lần duy nhất. Điều này rất quan trọng trong các tình huống như khi một yêu cầu bị mất và được gửi lại, đảm bảo rằng server không bị ảnh hưởng bởi các yêu cầu lặp lại.

* **Tính che giấu thông tin (Visibility)**

    Tính che giấu thông tin liên quan đến khả năng của phương thức trong việc truyền tải ý định của hành động thông qua tên phương thức. Điều này giúp các nhà phát triển và hệ thống hiểu rõ hơn về mục đích của yêu cầu.

* **Cacheable (Có thể cache được)**

    Một phương thức được coi là cacheable nếu kết quả của nó có thể được lưu trữ tạm thời để tái sử dụng trong các yêu cầu tương lai. Điều này giúp giảm tải cho server và cải thiện hiệu suất của ứng dụng.

Những tính chất này giúp đảm bảo rằng các phương thức HTTP được sử dụng một cách nhất quán và hiệu quả, tối ưu hóa quá trình phát triển và vận hành các ứng dụng web.

## 2. 9 method của HTTP

Trong giao thức HTTP, các phương thức (methods) được thiết kế để thực hiện các hành động cụ thể trên các tài nguyên web. Mỗi phương thức có những đặc điểm và cách sử dụng riêng biệt. Dưới đây là giải thích chi tiết về các phương thức HTTP chính, bao gồm GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE, và PATCH.

* **GET**

    Phương thức GET yêu cầu tài nguyên mục tiêu chuyển giao một đại diện của trạng thái của nó. Yêu cầu GET chỉ nên lấy dữ liệu và không có hiệu ứng nào khác.

    Phương thức GET được ưu tiên hơn POST khi lấy tài nguyên mà không làm thay đổi trạng thái của server vì nó có thể được gọi qua URL. Điều này cho phép đánh dấu trang (bookmark) và chia sẻ, cũng như làm cho các phản hồi GET có thể được cache, giúp tiết kiệm băng thông.

* **HEAD**

    Phương thức HEAD yêu cầu tài nguyên mục tiêu chuyển giao một đại diện của trạng thái, giống như yêu cầu GET, nhưng không có dữ liệu đại diện trong phản hồi.

    Điều này hữu ích để lấy metadata của đại diện trong header phản hồi mà không phải chuyển toàn bộ dữ liệu đại diện. Sử dụng bao gồm kiểm tra xem trang có sẵn thông qua mã trạng thái và nhanh chóng tìm kích thước của tệp (Content-Length).

* **POST**

    Phương thức POST yêu cầu tài nguyên mục tiêu xử lý đại diện được đính kèm trong yêu cầu theo ngữ nghĩa của tài nguyên mục tiêu.

* **PUT**

    Phương thức PUT yêu cầu tài nguyên mục tiêu tạo hoặc cập nhật trạng thái của nó với trạng thái được định nghĩa bởi đại diện đính kèm trong yêu cầu.

* **DELETE**

    Phương thức DELETE yêu cầu tài nguyên mục tiêu xóa trạng thái của nó.

* **CONNECT**

    Phương thức CONNECT yêu cầu trung gian thiết lập một kênh TCP/IP tới server gốc được xác định bởi mục tiêu yêu cầu. Nó thường được sử dụng để bảo mật kết nối thông qua một hoặc nhiều proxy HTTP với TLS.

* **OPTIONS**

    Phương thức OPTIONS yêu cầu tài nguyên mục tiêu chuyển giao các phương thức HTTP mà nó hỗ trợ. Thường được sử dụng để kiểm tra chức năng của một web server bằng cách yêu cầu '``*``' thay vì một tài nguyên cụ thể.

* **TRACE**

    Phương thức TRACE yêu cầu tài nguyên mục tiêu chuyển giao yêu cầu nhận được trong thân phản hồi. Điều này giúp client có thể thấy những thay đổi hoặc bổ sung nào đã được thực hiện bởi các trung gian, nếu có.

* **PATCH**
    
    Phương thức PATCH yêu cầu tài nguyên mục tiêu chỉnh sửa trạng thái của nó theo cập nhật từng phần được định nghĩa trong đại diện đính kèm trong yêu cầu. Phương thức này giúp tiết kiệm băng thông bằng cách cập nhật một phần của tệp hoặc tài liệu mà không phải chuyển toàn bộ dữ liệu.

| Phương thức | An toàn | Idempotent | Visibility        | Cacheable         |
|-------------|---------|------------|-------------------|-------------------|
| **GET**     | Có      | Có         | Lấy dữ liệu       | Có thể cache được |
| **HEAD**    | Có      | Có         | Kiểm tra tài nguyên| Có thể cache được |
| **POST**    | Không   | Không      | Gửi dữ liệu đến server | Không cache được |
| **PUT**     | Không   | Có         | Cập nhật hoặc tạo mới tài nguyên | Không cache được |
| **DELETE**  | Không   | Có         | Xóa tài nguyên    | Không cache được |
| **CONNECT** | Không   | Không      | Thiết lập kết nối TCP/IP | Không cache được |
| **OPTIONS** | Có      | Có         | Xác định phương thức hỗ trợ | Không cache được |
| **TRACE**   | Có      | Có         | Chẩn đoán đường đi của yêu cầu | Không cache được |
| **PATCH**   | Không   | Có thể không | Thay đổi một phần tài nguyên | Không cache được |


# II. Status code

Status Code là một số nguyên 3 ký tự, trong đó ký tự đầu tiên của mã hóa trạng thái định nghĩa hạng (loại) phản hồi và hai ký tự cuối không có bất cứ vai trò phân loại nào. Có 5 giá trị của ký tự đầu tiên như sau:

**1xx (100 – 199): Information responses / Phản hồi thông tin**


| Mã trạng thái | Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **100**| Continue| Máy chủ đã nhận được một phần của yêu cầu và máy khách nên tiếp tục gửi phần còn lại của yêu cầu.|
| **101**| Switching Protocols| Máy khách đã yêu cầu máy chủ chuyển đổi giao thức và máy chủ xác nhận rằng nó sẽ làm như vậy.|
| **102**| Processing| Máy chủ đã nhận được yêu cầu nhưng vẫn đang xử lý nó và chưa có phản hồi hoàn chỉnh.                      |
| **103**| Early Hints| Được sử dụng để trả về một số header phản hồi trước khi phản hồi HTTP thực sự hoàn chỉnh được gửi đến.    |

**2xx (200 – 299): Successful responses / Phản hồi thành công**

| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **200**| OK| Yêu cầu đã thành công và máy chủ đã trả về tài nguyên yêu cầu.       |
| **201**| Created| Yêu cầu đã thành công và một tài nguyên mới đã được tạo ra.          |
| **202**| Accepted| Yêu cầu đã được chấp nhận để xử lý, nhưng việc xử lý chưa hoàn tất.   |
| **204**| No Content| Yêu cầu đã thành công nhưng không có nội dung nào được trả về.       |
| **206**| Partial Content| Máy chủ chỉ trả về một phần của tài nguyên do phạm vi tiêu đề được gửi bởi máy khách. |

**3xx (300 – 399): Redirects / Điều hướng**


| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **301**| Moved Permanently| Tài nguyên yêu cầu đã được di chuyển vĩnh viễn đến URL mới.|
| **302**| Found| Tài nguyên yêu cầu tạm thời được di chuyển đến URL mới.|
| **303**| See Other| Máy khách nên dùng GET để yêu cầu tài nguyên ở URL khác.|
| **304**| Not Modified| Tài nguyên không có sự thay đổi kể từ lần truy cập cuối.|
| **307**| Temporary Redirect| Tài nguyên yêu cầu tạm thời được di chuyển đến URL khác, nhưng phương thức HTTP không thay đổi. |
| **308**| Permanent Redirect| Tài nguyên yêu cầu đã được di chuyển vĩnh viễn đến URL mới và phương thức HTTP không thay đổi. |

**4xx (400 – 499): Client errors / Lỗi phía client**


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

**5xx (500 – 599): Server errors / Lỗi phía máy chủ**


| Mã trạng thái| Cụm từ giải thích| Mô tả|
|---------------|------------------------|----------------------------------------------------------------------|
| **500**| Internal Server Error| Máy chủ gặp lỗi và không thể hoàn thành yêu cầu.|
| **501**| Not Implemented| Máy chủ không hỗ trợ chức năng cần thiết để hoàn thành yêu cầu.|
| **502**| Bad Gateway| Máy chủ hoạt động như một cổng hoặc proxy và nhận được phản hồi không hợp lệ từ máy chủ ngược lại. |
| **503**| Service Unavailable| Máy chủ hiện không thể xử lý yêu cầu do quá tải hoặc bảo trì.|
| **504**| Gateway Timeout| Máy chủ hoạt động như một cổng hoặc proxy và không nhận được phản hồi kịp thời từ máy chủ ngược lại. |
| **505**| HTTP Version Not Supported | Máy chủ không hỗ trợ phiên bản HTTP được sử dụng trong yêu cầu.|

# END