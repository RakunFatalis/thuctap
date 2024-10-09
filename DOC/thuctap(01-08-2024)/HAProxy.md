# HAProxy

# Mục lục 

- [HAProxy](#haproxy)
- [Mục lục](#mục-lục)
- [I. HAProxy là gì?](#i-haproxy-là-gì)
- [II. Các loại cân bằng tải của HAProxy](#ii-các-loại-cân-bằng-tải-của-haproxy)
  - [1. Không có cân bằng tải](#1-không-có-cân-bằng-tải)
  - [2. Cân bằng tải tại tầng 4 (tầng truyền vận)](#2-cân-bằng-tải-tại-tầng-4-tầng-truyền-vận)
  - [3. Cân bằng tải tại tầng 7 (tầng ứng dụng)](#3-cân-bằng-tải-tại-tầng-7-tầng-ứng-dụng)
  - [4. Bảng so sánh](#4-bảng-so-sánh)
- [III. Các thuật toán trong cân bằng tải](#iii-các-thuật-toán-trong-cân-bằng-tải)
- [IV. Các thuật ngữ cân bằng tải](#iv-các-thuật-ngữ-cân-bằng-tải)
  - [1. Access Control List (ACL)](#1-access-control-list-acl)
  - [2. Backend](#2-backend)
  - [3. Frontend](#3-frontend)
- [END](#end)

# I. HAProxy là gì?

![](/img/HAProxy_logo.png)

**HAProxy (High Availability Proxy)** là một phần mềm mã nguồn mở, miễn phí, rất nhanh và đáng tin cậy, cung cấp proxy ngược, cân bằng tải và proxy cho các ứng dụng dựa trên TCP và HTTP. Nó đặc biệt phù hợp cho các trang web có lưu lượng truy cập rất cao và là công cụ phổ biến cho một phần lớn các trang web được truy cập nhiều nhất trên thế giới. Qua nhiều năm, HAProxy đã trở thành tiêu chuẩn mặc định cho bộ cân bằng tải mã nguồn mở, được tích hợp trong hầu hết các bản phân phối Linux chính thống và thường được triển khai mặc định trên các nền tảng đám mây. Vì nó không tự quảng cáo, nên chúng ta chỉ biết đến nó khi các quản trị viên nói về nó.

Nhóm phát triển cốt lõi của HAProxy duy trì nhiều phiên bản cùng một lúc. Kể từ phiên bản ``1.8``, mỗi năm có hai phiên bản chính được phát hành. Chữ số đầu tiên thường chỉ ra một thay đổi phá vỡ (như định dạng cấu hình v.v.) nhưng trong thực tế hiếm khi thay đổi. Chữ số thứ hai chỉ ra các tính năng mới. Cả hai tạo thành một nhánh. Một số thêm xuất hiện sau các chữ số này để chỉ ra phiên bản sửa lỗi.

Nhóm phát triển đầu tư rất nhiều công sức vào việc đưa các bản vá lỗi cho các phiên bản cũ hơn trong khi cực kỳ cẩn thận để không phá vỡ bất cứ điều gì. Vì lý do này, rất quan trọng để cập nhật trong một nhánh, tức là có số cao nhất có thể ở chữ số cuối cùng.

Các nhánh có số chẵn được gọi là "``LTS``" (hỗ trợ dài hạn) và được duy trì trong 5 năm sau khi phát hành. Trong thời gian này, chúng sẽ nhận được các bản vá lỗi được phát hiện sau khi phát hành. Các nhánh này nhằm vào người dùng phổ thông muốn sự ổn định cao và không muốn cập nhật phiên bản mới quá thường xuyên nhưng vẫn muốn nhận các bản vá lỗi.

Các nhánh có số lẻ thì được gọi là "``stable``" (ổn định), nhằm vào người dùng có kỹ năng cao muốn cập nhật thường xuyên để hưởng lợi từ các tính năng hiện đại và cũng có khả năng quay lại phiên bản trước đó nếu gặp sự cố. Các phiên bản này được duy trì trong khoảng 12 đến 18 tháng. Thời gian này ngắn và không cố định để chu kỳ bảo trì được quyết định dựa trên phản hồi của người dùng, và để các phiên bản này không kết thúc trong các sản phẩm nhúng. Có thể một số tính năng sẽ được đưa vào lại các phiên bản này nếu có nhu cầu hợp lý và hoạt động được coi là đủ an toàn.

Những người có kinh nghiệm trong việc triển khai sản phẩm biết rằng rất khó để nâng cấp các thành phần khi phải lên kế hoạch và thông báo trước về bất kỳ hoạt động nào. Vì lý do này, nhóm phát triển cốt lõi của HAProxy không nhấn mạnh vào việc người dùng nâng cấp, không yêu cầu ai đó chuyển sang nhánh mới (trừ khi họ yêu cầu một tính năng nằm trong nhánh đó), nhưng sẽ thường yêu cầu người dùng kiểm tra lại với phiên bản mới nhất của nhánh của họ trước khi báo cáo một vấn đề, vì không ai thích phải xử lý lại một vấn đề lần thứ hai. Thường được đề nghị sử dụng các phiên bản đi kèm với hệ điều hành khi nó tuân theo chu kỳ bảo trì chính thức, và tùy thuộc vào mức độ ổn định hoặc phơi nhiễm mong đợi, một số người dùng có thể muốn cập nhật ngay khi có bản cập nhật trong khi những người khác có thể chờ vài tuần đến một tháng để đảm bảo rằng bản cập nhật đủ đáng tin cậy đối với họ.

# II. Các loại cân bằng tải của HAProxy

Cân bằng tải là phương thức phân phối lưu lượng truy cập mạng đều nhau trên một vùng tài nguyên hỗ trợ ứng dụng.
Trong HAProxy ta có 3 loại cân bằng tải.

## 1. Không có cân bằng tải

Đây là một mô hình cơ bản nhất cho một ứng dụng web, thường được áp dụng trong môi trường có số lượng người dùng ít hoặc không có, sử dụng cho mục đích thử nghiệm hoặc phát triển.

![](/img/HAProxy_noloadbalancing.png)

Với mô hình này, người dùng sẽ kết nối trực tiếp với web server tại ``yourdomain.com`` và không có cân bằng tải nào được sử dụng. Nếu webserver gặp trục trặc, người dùng sẽ không thể kết nối đến ứng dụng web được nữa.

## 2. Cân bằng tải tại tầng 4 (tầng truyền vận)

Cách đơn giản nhất để có thể cân bằng tải tới nhiều server là sử dụng cân bằng tải trên tầng 4. Theo hướng này thì các request sẽ được điều hướng dựa trên khoảng địa chỉ IP và cổng (ví dụ một request tới địa chỉ ``http:://www.example.com/something`` sẽ được điều hướng tới backend được dùng để điều hướng cho domain example.com với cổng 80)

![](/img/HAProxy_layer%204%20load.png)

Người dùng truy cập vào bộ cân bằng tải, bộ này sẽ chuyển tiếp yêu cầu của người dùng đến nhóm máy chủ backend web. Máy chủ backend nào được chọn sẽ phản hồi trực tiếp yêu cầu của người dùng. Thông thường, tất cả các máy chủ trong nhóm backend web nên phục vụ nội dung giống nhau – nếu không, người dùng có thể nhận được nội dung không nhất quán. Lưu ý rằng cả hai máy chủ web đều kết nối đến cùng một máy chủ cơ sở dữ liệu.

## 3. Cân bằng tải tại tầng 7 (tầng ứng dụng)

Cân bằng tải tại tầng 7 là cách cân bằng tải phức tạp nhất và cũng là cách cân bằng tải có nhiều tùy biến nhất. Sử dụng cân bằng tải tại tầng 7, ta có thể điều hướng request dựa trên nội dụng của request đó. Với kiểu câng bằng tải này, nhiều backend có thể được sử dụng cho dùng một domain và port.

![](/thuctap/img/HAProxy_layer%207%20load.png)

## 4. Bảng so sánh

| Một số loại cân bằng tải| Mô tả| Ưu điểm| Nhược điểm|
|-------------------------|------|--------|-----------|
| **No Load Balancing** |Mọi lưu lượng truy cập đều được gửi trực tiếp đến một máy chủ duy nhất.| Đơn giản, cài đặt và cấu hình đơn giản| Khả năng mở rộng thấp, không có khả năng chịu lỗi, hiệu suất thấp khi lưu lượng truy cập cao|
| **Layer 4 Load Balancing** | Cân bằng tải dựa trên địa chỉ IP và cổng TCP/UDP.| Hiệu suất cao, khả năng mở rộng tốt, dễ cài đặt và cấu hình| Không có khả năng phân biệt các ứng dụng khác nhau trên cùng một máy chủ, không có khả năng xử lý các yêu cầu HTTP phức tạp |
| **Layer 7 Load Balancing** | Cân bằng tải dựa trên nội dung yêu cầu HTTP, bao gồm URL, cookie, header, v.v.| Khả năng phân biệt các ứng dụng khác nhau trên cùng một máy chủ, khả năng xử lý các yêu cầu HTTP phức tạp |Phức tạp hơn để cài đặt và cấu hình, hiệu suất có thể thấp hơn so với Layer 4 Load Balancing


# III. Các thuật toán trong cân bằng tải

| Thuật toán| Mô tả| Ưu điểm| Nhược điểm|
|-----------|------|--------|-----------|
| **Round robin**| Phân phối các yêu cầu đến các máy chủ backend theo thứ tự tuần tự.| Đơn giản, cân bằng tải đều| Không phù hợp với các yêu cầu có thời gian xử lý khác nhau |
| **Least conn**| Gửi yêu cầu mới đến máy chủ có ít kết nối nhất hiện tại.| Hiệu quả cho các dịch vụ có thời gian xử lý thay đổi| Cần giám sát và cập nhật số lượng kết nối hiện tại|
| **Source**| Dựa trên địa chỉ IP của nguồn yêu cầu, đảm bảo rằng các yêu cầu từ cùng một IP luôn đến cùng một máy chủ. | Phù hợp cho việc duy trì phiên| Không cân bằng tải đều|
| **First**| Gửi tất cả các yêu cầu đến máy chủ đầu tiên đang hoạt động trong danh sách.| Dễ cài đặt và cấu hình| Không cân bằng tải, không chịu lỗi cao|
| **Static-rr**| Cân bằng tải dựa trên danh sách máy chủ tĩnh với phân bổ trọng số cụ thể.| Phân phối tải theo trọng số| Phải cấu hình lại khi thay đổi trạng thái máy chủ|
| **URI**| Dựa trên URI của yêu cầu, đảm bảo rằng các yêu cầu với cùng một URI sẽ luôn đến cùng một máy chủ. | Hữu ích cho các hệ thống cache| Cần cấu hình và giám sát kỹ lưỡng|
| **Hdr(name)**| Dựa trên giá trị của một tiêu đề HTTP cụ thể (header) trong yêu cầu.| Linh hoạt theo giá trị header| Cấu hình phức tạp, cần kiểm tra kỹ giá trị header|
| **Rdp-cookie(name)**| Sử dụng giá trị của cookie trong giao thức RDP để duy trì phiên giữa client và server. | Phù hợp cho các môi trường Remote Desktop Protocol (RDP)| Giới hạn cho các ứng dụng sử dụng RDP|

# IV. Các thuật ngữ cân bằng tải

## 1. Access Control List (ACL)

Trong cân bằng tải, ACL được dùng để kiểm tra điều kiện và thực hiện một hành động (ví dụ như lựa chọn một server hay chặn một request) dựa trên kết quả của việc kiểm tra đó. Việc sử dụng ACL cho phép tạo một môi trường có khả năng chuyển tiếp các request một cách linh hoạt dựa trên các yếu tố khác nhau mà người dùng có thể tùy chỉnh một cách dễ dàng.

## 2. Backend

Backend là một tập các server mà HAProxy có thể forward các request tới. Backend được cấu hình trong mục backend trong file configuration của HAProxy. Ở dạng đơn giản nhất, một backend có thể được cài đặt bằng cách

* Đặt ra thuật toán để căn bằng tải (round-robin, least-connection,...)

* Một danh sách các máy chủ và port của chúng có thể dùng để nhận request từ HAProxy

Một backend có thể chứa một hoặc nhiều server, về cơ bản thì càng nhiều server trong một backend thì khả năng chịu tải và performance của hệ thống càng tăng lên. Tính tin cậy của hệ thống cũng tăng lên theo phương pháp này vì khi một server bị ngắt khỏi proxy, các server có thể chịu tải thay được cho nó.
HAProxy còn cho phép một server backup chuyên dụng, được sử dụng khi các server đều offline. Server backup này thường sẽ chứa các thông báo hệ thống offline hoặc một thông điệp nào đó để người dùng có thể biết được rằng hệ thống đang tạm thời không có sẵn.

## 3. Frontend

Frontend được dùng để định nghĩa cách mà các request được điều hướng cho backend. Frontend được định nghĩa trong mục frontend của HAProxy configuration. Các cấu hình cho frontend gồm:

* Một bộ địa chỉ IP và port (ví dụ: 10.0.0.1:8080, *:443,...)

* Các ACL do người dùng định nghĩa

* Backend được dùng để nhận request

# END