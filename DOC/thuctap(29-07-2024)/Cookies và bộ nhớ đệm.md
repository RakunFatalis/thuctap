# Cookies và bộ nhớ đệm

# Mục lục

- [Cookies và bộ nhớ đệm](#cookies-và-bộ-nhớ-đệm)
- [Mục lục](#mục-lục)
- [I. Cookies là gì ?](#i-cookies-là-gì-)
- [II. Cookies thường dùng để làm gì ?](#ii-cookies-thường-dùng-để-làm-gì-)
- [III. Bộ nhớ đệm là gì ?](#iii-bộ-nhớ-đệm-là-gì-)

# I. Cookies là gì ?

Cookies là những tập tin nhỏ chứa thông tin mà máy chủ web tạo ra và gửi đến trình duyệt web. Các trình duyệt web lưu trữ cookies mà chúng nhận được trong một khoảng thời gian xác định trước, hoặc trong suốt thời gian người dùng phiên làm việc trên trang web. Chúng đính kèm cookies liên quan vào bất kỳ yêu cầu nào mà người dùng gửi đến máy chủ web sau này.

Cookies giúp các trang web nhận diện người dùng, cho phép các trang web cá nhân hóa trải nghiệm của người dùng. Ví dụ, các trang web thương mại điện tử sử dụng cookies để biết các mặt hàng mà người dùng đã đặt vào giỏ hàng của họ. Ngoài ra, một số cookies là cần thiết cho các mục đích bảo mật, chẳng hạn như cookies xác thực (xem dưới đây).

Những cookies được sử dụng trên Internet cũng được gọi là "HTTP cookies." Giống như nhiều phần khác của web, cookies được gửi qua giao thức HTTP.

# II. Cookies thường dùng để làm gì ?

Máy chủ thường sử dụng nội dung của HTTP cookies để xác định liệu các yêu cầu khác nhau có đến từ cùng một trình duyệt/người dùng hay không, và sau đó đưa ra phản hồi cá nhân hóa hoặc chung chung tùy thuộc vào tình trạng.

Sau đây mô tả một hệ thống đăng nhập người dùng rất đơn giản:

1. Người dùng gửi thông tin đăng nhập đến máy chủ, chẳng hạn qua việc gửi biểu mẫu.

2. Nếu thông tin đăng nhập là chính xác, máy chủ cập nhật giao diện người dùng để cho biết rằng người dùng đã đăng nhập, và phản hồi bằng một cookie chứa ID phiên (session ID) ghi lại trạng thái đăng nhập của họ trên trình duyệt.

3. Sau một thời gian, người dùng chuyển đến một trang khác trên cùng một trang web. Trình duyệt gửi cookie chứa ID phiên cùng với yêu cầu tương ứng để cho biết rằng nó vẫn cho rằng người dùng đã đăng nhập.

4. Máy chủ kiểm tra ID phiên và nếu nó vẫn hợp lệ, gửi cho người dùng phiên bản cá nhân hóa của trang mới. Nếu không hợp lệ, ID phiên bị xóa và người dùng sẽ được hiển thị phiên bản chung của trang (hoặc có thể nhận được thông báo "truy cập bị từ chối" và yêu cầu đăng nhập lại).

![](/img/Cookies.png)

Cookies chủ yếu được sử dụng cho ba mục đích sau:

*** Quản lý phiên làm việc**: Trạng thái đăng nhập của người dùng, nội dung giỏ hàng, điểm số trò chơi, hoặc bất kỳ chi tiết liên quan đến phiên làm việc của người dùng mà máy chủ cần nhớ.

* **Cá nhân hóa**: Sở thích của người dùng như ngôn ngữ hiển thị và chủ đề giao diện người dùng.

* **Theo dõi**: Ghi lại và phân tích hành vi của người dùng.


# III. Bộ nhớ đệm là gì ?

Cache hay còn được gọi là bộ nhớ đệm. Nó là phần cứng, hoặc có khi là phần mềm tích hợp sẵn trong máy tính để lưu trữ dữ liệu tạm thời.

Caching chính là hoạt động lưu trữ dữ liệu dạng nhị phân vào cache. Điều này giúp rút ngắn thời gian truy cập bằng cách tăng tốc độ và giảm độ trễ của webiste, đồng thời, các thao tác trên website cũng thuận tiện và nhanh hơn. Các workload hầu hết của ứng dụng đều sẽ phụ thuộc vào tốc độ đầu vào (input)/đầu ra (output). Cache thường được dùng để cải thiện hiệu suất cho các ứng dụng, website có lượt truy cập cao.

**Ưu và nhược của cache**


**Ưu điểm**

1. **Tăng Tốc Độ Truy Cập:**

   * Giảm Thời Gian Tải: Cache lưu trữ dữ liệu gần gũi hơn với người dùng hoặc ứng dụng, giúp giảm thời gian truy cập dữ liệu.
   
   * Tăng Hiệu Suất: Giúp giảm độ trễ và cải thiện hiệu suất của ứng dụng hoặc trang web.

2. **Giảm Tải Cho Máy Chủ:**

   * Giảm Số Lượng Yêu Cầu Đến Máy Chủ: Khi dữ liệu được lưu trữ trong cache, số lượng yêu cầu gửi đến máy chủ gốc giảm, giúp giảm tải và bảo vệ máy chủ khỏi quá tải.

3. **Tiết Kiệm Tài Nguyên:**

   * Giảm Đường Truyền: Giảm băng thông cần thiết cho việc truyền tải dữ liệu từ máy chủ gốc.

   * Tiết Kiệm Chi Phí: Ít tốn kém hơn trong việc xử lý các yêu cầu liên tục từ máy chủ gốc.

4. **Cải Thiện Trải Nghiệm Người Dùng:**

   * Phản Hồi Nhanh Hơn: Người dùng trải nghiệm trang web hoặc ứng dụng nhanh hơn do dữ liệu được lấy từ cache.


**Nhược điểm**

1. **Dữ Liệu Cũ:**

   * Khả Năng Lưu Trữ Dữ Liệu Lỗi Thời: Dữ liệu trong cache có thể trở nên lỗi thời nếu không được cập nhật thường xuyên, dẫn đến việc người dùng thấy thông tin không chính xác.

2. **Khó Quản Lý:**

   * Quản Lý Dữ Liệu: Cần phải có cơ chế để quản lý, làm mới và xóa dữ liệu cache, đặc biệt là khi có nhiều loại dữ liệu và các chính sách lưu trữ khác nhau.

3. **Chi Phí Lưu Trữ:**

   * Tốn Kém Tài Nguyên: Cache yêu cầu tài nguyên lưu trữ bổ sung, điều này có thể dẫn đến chi phí tăng lên nếu không được quản lý đúng cách.

4. **Vấn Đề Bảo Mật:**

   * Rủi Ro Bảo Mật: Dữ liệu nhạy cảm có thể bị lưu trữ trong cache, gây rủi ro bảo mật nếu không được bảo vệ đúng cách.

5. **Sự Phức Tạp Trong Thiết Kế:**

   * Thiết Kế Hệ Thống: Việc tích hợp và duy trì cache có thể làm cho thiết kế hệ thống trở nên phức tạp hơn, đặc biệt khi cần đồng bộ hóa dữ liệu giữa cache và máy chủ gốc.