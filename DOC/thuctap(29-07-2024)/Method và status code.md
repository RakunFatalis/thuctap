# Method và status code

# Mục lục


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

Dưới đây là bảng liệt kê một số mã thường gặp