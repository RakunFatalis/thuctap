# DNS

# MỤC LỤC

- [DNS](#dns)
- [MỤC LỤC](#mục-lục)
  - [I. DNS là gì, DNS hoạt động như thế nào?](#i-dns-là-gì-dns-hoạt-động-như-thế-nào)
    - [1. DNS là gì.](#1-dns-là-gì)
    - [2. DNS hoạt động như thế nào?](#2-dns-hoạt-động-như-thế-nào)
  - [II. Các bản ghi của DNS](#ii-các-bản-ghi-của-dns)
  - [III. Các loại và phương pháp phân giải DNS](#iii-các-loại-và-phương-pháp-phân-giải-dns)
    - [1. Primary DNS và Secondary DNS](#1-primary-dns-và-secondary-dns)
    - [2. Round Robin DNS](#2-round-robin-dns)
    - [3. Reverse DNS](#3-reverse-dns)
- [END](#end)







## I. DNS là gì, DNS hoạt động như thế nào?

### 1. DNS là gì.

Hệ thống phân giải tên miền (hay được viết tắt là DNS do tên tiếng Anh Domain Name System) là một hệ thống cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền trên Internet.

DNS về căn bản là một hệ thống giúp cho việc chuyển đổi các tên miền mà con người dễ ghi nhớ (dạng ký tự, ví dụ www.example.com) sang địa chỉ IP vật lý (dạng số, ví dụ 123.11.5.19) tương ứng của tên miền đó. DNS giúp liên kết với các trang thiết bị mạng cho các mục đích định vị và địa chỉ hóa các thiết bị trên Internet.

Phép so sánh thường được sử dụng để giải thích cho DNS là, nó phục vụ như một "Danh bạ điện thoại", có khả năng tìm kiếm và dịch tên miền thành địa chỉ IP. Ví dụ, www.example.com dịch thành 208.77.188.166. Tên miền Internet dễ nhớ hơn các địa chỉ IP, là ``208.77.188.166`` (IPv4) hoặc ``2400:cb00:2048:1::c629:d7a2`` (IPv6).

Hệ thống phân giải tên miền phân phối trách nhiệm gán tên miền và lập bản đồ những tên tới địa chỉ IP bằng cách định rõ những máy chủ có thẩm quyền cho mỗi tên miền. Những máy chủ có tên thẩm quyền được phân công chịu trách nhiệm đối với tên miền riêng của họ, và lần lượt có thể chỉ định tên máy chủ khác độc quyền của họ cho các tên miền phụ. Kỹ thuật này đã thực hiện các cơ chế phân phối DNS, chịu đựng lỗi, và giúp tránh sự cần thiết cho một trung tâm đơn lẻ để đăng ký được tư vấn và liên tục cập nhật.

### 2. DNS hoạt động như thế nào?

Quá trình phân giải DNS liên quan đến việc chuyển đổi một tên miền (chẳng hạn như www.example.com) thành một địa chỉ IP thân thiện với máy tính (chẳng hạn như 192.168.1.1). Mỗi thiết bị trên Internet được gán một địa chỉ IP, và địa chỉ này cần thiết để tìm thiết bị Internet tương ứng - giống như địa chỉ nhà dùng để tìm một ngôi nhà cụ thể. Khi người dùng muốn tải một trang web, cần phải có một quá trình chuyển đổi giữa những gì người dùng nhập vào trình duyệt web (ví dụ: example.com) và địa chỉ thân thiện với máy cần thiết để định vị trang web example.com.

**Các bước chi tiết trong quá trình phân giải DNS:**

* **Yêu cầu từ trình duyệt**: Khi người dùng nhập tên miền vào trình duyệt, một yêu cầu DNS sẽ được gửi đi.


* **Kiểm tra cache của trình duyệt**: Trình duyệt kiểm tra cache của chính nó để xem có bản ghi DNS tương ứng không.

* **Kiểm tra cache của hệ điều hành**: Nếu trình duyệt không có bản ghi, hệ điều hành sẽ kiểm tra cache của nó.

* **Truy vấn tới DNS Resolver**: Nếu không tìm thấy kết quả trong cache, hệ điều hành sẽ gửi truy vấn tới DNS Resolver (thường do nhà cung cấp dịch vụ Internet - ISP - quản lý).

* **Truy vấn Root DNS Server**: DNS Resolver gửi truy vấn tới một trong các Root DNS Server nếu nó không có câu trả lời trong cache.

* **Truy vấn TLD DNS Server**: Root DNS Server trả về địa chỉ của Top-Level Domain (TLD) DNS Server (ví dụ: .com, .net).

* **Truy vấn Authoritative DNS Server**: TLD DNS Server trả về địa chỉ của Authoritative DNS Server, nơi lưu trữ bản ghi DNS cho tên miền cụ thể.

* **Trả về địa chỉ IP**: Authoritative DNS Server trả về địa chỉ IP tương ứng với tên miền.

**Sau khi địa chỉ IP được trả về**:

* **Lưu vào cache**: DNS Resolver lưu kết quả vào cache của nó và trả kết quả về cho hệ điều hành.

* **Hệ điều hành lưu cache**: Hệ điều hành lưu cache và trả kết quả về trình duyệt.

* **Truy cập trang web**: Trình duyệt sử dụng địa chỉ IP này để gửi yêu cầu đến máy chủ đích và tải trang web về.

## II. Các bản ghi của DNS

Các bản ghi DNS (DNS records) là các mục trong cơ sở dữ liệu của DNS, cung cấp thông tin về tên miền, địa chỉ IP, và các thông tin liên quan khác. Dưới đây là một số bản ghi phổ biến.

* **Bản ghi A (A Record)**

    Bản ghi A là một loại bản ghi DNS được sử dụng để ánh xạ một tên miền cụ thể sang địa chỉ IP tương ứng. Bản ghi A (Address Record) chứa thông tin về địa chỉ IPv4 của máy chủ hoặc tài nguyên được chỉ định bởi tên miền đó.

    Khi bạn truy cập một trang web hoặc gửi yêu cầu đến một máy chủ thông qua tên miền, hệ thống DNS sử dụng bản ghi A để tìm và trả về địa chỉ IPv4 tương ứng của máy chủ đó. Sau đó, trình duyệt hoặc ứng dụng có thể sử dụng địa chỉ IP này để thiết lập kết nối và truy cập tài nguyên trên mạng.

* **Bản ghi AAAA**

    Bản ghi A là một loại bản ghi DNS được sử dụng để ánh xạ một tên miền cụ thể sang địa chỉ IPv6 tương ứng. Bản ghi AAAA giống như bản ghi A, ngoại trừ việc chúng lưu trữ địa chỉ IPv6 của miền thay vì địa chỉ IPv4 của tên miền đó.

* **Bản ghi NS (Name Server Record)**

    Bản ghi NS (Name Server Record) là một loại bản ghi được sử dụng để xác định máy chủ tên miền chịu trách nhiệm quản lý một tên miền cụ thể trên Internet. Bản ghi NS cung cấp thông tin về các máy chủ định danh chính (primary name server) và máy chủ định danh phụ (secondary name server) cho một tên miền cụ thể.

    Khi bạn truy cập một trang web hoặc gửi một email, hệ thống DNS sẽ sử dụng bản ghi NS để xác định máy chủ DNS nào sẽ cung cấp thông tin về tên miền đó. Các bản ghi NS này giúp tổ chức Internet duyệt thông tin truy vấn DNS từ tên miền và tìm ra địa chỉ IP tương ứng của máy chủ hoặc dịch vụ.

* **Bản ghi CNAME (Canonical name Record)**

    Bản ghi CNAME cho phép một server có thể có nhiều tên. Nói cách khác bản ghi CNAME cho phép nhiều tên miền cùng trỏ đến một địa chỉ IP cho trước.

    Để có thể khai báo bản ghi CNAME, **bắt buộc phải có bản ghi kiểu A** để khai báo tên của máy. Tên miền được khai báo trong bản ghi kiểu A trỏ đến địa chỉ IP của máy được gọi là tên miền chính (canonical domain). Các tên miền khác muốn trỏ đến máy tính này phải được khai báo là bí danh của tên máy (alias domain).

* **Bản ghi MX (MX Record)**

    Bản ghi MX được sử dụng để định vị Mail server cho một tên miền. Người ta có thể gán nhiều MX record cho một tên miền. Do đó, Email của bạn sẽ không bị mất dữ liệu nếu ngừng hoạt động một thời gian.

* **Bản ghi TXT**

    Bản ghi TXT được sử dụng để lưu trữ thông tin văn bản tùy chỉnh cho một tên miền cụ thể. Bản ghi TXT chứa các dòng văn bản không định dạng cụ thể và thường được sử dụng để lưu trữ các thông tin liên quan đến tên miền, như xác thực, xác định quyền sở hữu, và các thông tin khác mà các dịch vụ và ứng dụng trực tuyến có thể sử dụng.

* **Bản ghi PTR (Pointer Record)**

    Bản ghi PTR được sử dụng để ánh xạ một địa chỉ IP (IPv4 hoặc IPv6) thành một tên miền. Bản ghi PTR hoạt động theo chiều ngược lại so với các bản ghi DNS thông thường: thay vì ánh xạ tên miền thành địa chỉ IP (như trong bản ghi A hoặc AAAA), nó ánh xạ địa chỉ IP thành tên miền. 

* **Bản ghi SOA (Start of Authority)**

    Bản ghi chỉ định thông tin có thẩm quyền về vùng DNS, bao gồm máy chủ DNS chính, email của quản trị viên tên miền, số sê-ri tên miền và một số bộ định thời liên quan đến làm mới vùng DNS. Chỉ có một bản ghi SOA trong vùng DNS miền.

* **Bản ghi SRV (Service Record)**

    Là một loại bản ghi trong hệ thống DNS được sử dụng để chỉ định dịch vụ và máy chủ cung cấp dịch vụ cụ thể cho một tên miền. Bản ghi SRV thường được sử dụng để hỗ trợ tự động cấu hình và khám phá các dịch vụ mạng trong môi trường mạng.

* **Bản ghi SPF(Sender Policy Framework)**

    Bản ghi SPF thực chất là loại bản ghi TXT, được sử dụng để xác định các máy chủ email được ủy quyền để gửi email từ tên miền cụ thể. SPF là một phần quan trọng của quá trình xác minh email và giúp ngăn chặn việc gửi email giả mạo từ tên miền của bạn.

    Bản ghi SPF chứa thông tin về các máy chủ email được phép gửi email từ tên miền của bạn bằng cách chỉ định các địa chỉ IP hoặc tên miền của những máy chủ này. Khi một máy chủ email nhận một email từ tên miền của bạn, nó có thể truy vấn DNS để kiểm tra xem máy chủ gửi email có phải là một máy chủ được ủy quyền theo SPF hay không.

* **Bản ghi DKIM (DomainKeys Identified Mail)**

    Bản ghi DKIM thực chất là loại bản ghi TXT, được sử dụng để cung cấp xác thực và đáng tin cậy cho email gửi từ một tên miền cụ thể. Bản ghi DKIM là một phần quan trọng của các hệ thống xác thực email và giúp ngăn chặn spam và email giả mạo.

    Bản ghi DKIM chứa các thông tin về chữ ký số được sử dụng để xác thực email gửi từ tên miền của bạn.

* **Bản ghi DMARC (Domain-based Message Authentication, Reporting, and Conformance)**

    Bản ghi DMARC thực chất là loại bản ghi TXT, được sử dụng để cung cấp hướng dẫn cho các máy chủ email về cách xử lý email gửi từ tên miền cụ thể. Bản ghi DMARC là một phần quan trọng của các hệ thống xác thực email và giúp cải thiện tính xác thực và bảo mật trong việc gửi và nhận email.

    Bản ghi DMARC chứa các thông tin về cách xử lý email gửi từ tên miền của bạn và có thể xác định các hành động cụ thể nếu email không đáp ứng các tiêu chuẩn xác thực SPF và DKIM. Cùng với DKIM và SPF, DMARC có chức năng giống như kiểm tra lý lịch về người gửi email, để đảm bảo rằng email thực sự là đúng người gửi.


## III. Các loại và phương pháp phân giải DNS

### 1. Primary DNS và Secondary DNS

* **Primary DNS**

    Có vai trò xác thực các thông tin chính thức của tên miền mà nó quản lý. Primary DNS còn được hiểu là máy chủ tên miền chính, ngoài ra còn có máy chủ tên miền phụ (Secondary DNS Server - SDS).

    Các thông tin, tên miền mà Primary DNS quản lý sẽ được khởi tạo, lưu trữ và xử lý tại đây, sau đó được chuyển sang các SDS.

* **Secondary DNS**

    Đây là một DNS  được sử dụng để thay thế cho Primary DNS bằng cách sao lưu lại tất cả bản ghi dữ liệu trên Primary Name server và nếu Primary Name server bị gián đoạn thì nó sẽ đảm nhận việc phần giải ánh xạ tên miền và địa chỉ IP.

### 2. Round Robin DNS

Round Robin DNS là một kỹ thuật phân phối tải, cân bằng tải hoặc fault-tolerance dự phòng, các máy chủ dịch vụ giao thức Internet dự phòng redundant Internet Protocol service, quản lý các phản hồi (DNS) của Hệ thống Tên miền đối với các yêu cầu địa chỉ từ máy khách theo một mô hình thống kê thích hợp.

Phương pháp Round Robin DNS là một phương pháp cân bằng tải phổ biến, đơn giản và dễ sử dụng; đặc biệt phương pháp này rất thích hợp khi cân bằng tải theo khu vực địa lý (Global Server Load Balancing).

Round robin DNS được sử dụng để tải các yêu cầu giúp cân bằng giữa một số máy chủ Web. Ví dụ: một công ty có một tên miền và 3 bản sao giống hệt nhau của cùng một trang web trên 3 máy chủ với ba địa chỉ IP khác nhau. Khi một người dùng cố gắng truy cập trang chủ, nó sẽ được gửi đến địa chỉ IP đầu tiên. Người dùng thứ 2 cố gắng truy cập trang chủ sẽ được gửi đến địa chỉ IP tiếp theo và người dùng thứ 3 sẽ được gửi đến địa chỉ IP thứ 3. Trong từng trường hợp, một địa chỉ IP được chuyển đến cho đến cuối danh sách được cấu hình. Người dùng thứ 4 sẽ được gửi đến địa chỉ IP đầu tiên.

### 3. Reverse DNS

Reverse DNS phục vụ cho việc xác định domain tương ứng với địa chỉ IP bằng cách truy vấn tên miền liên quan. Kỹ thuật Reverse DNS được sử dụng chủ yếu để kiểm tra tính chính xác của địa chỉ IP và hạn chế làm giả thông tin nguồn gốc của địa chỉ IP.

Nếu một trang web có cấu hình phân giải đảo DNS, người dùng có thể truy cập trang web đó bằng cách nhập địa chỉ IP của trang web vào thanh tìm kiếm thay vì tên miền. Ví dụ, nếu nhập địa chỉ IP 173.194.217.103 vào thanh tìm kiếm của trình duyệt, bạn sẽ được chuyển đến trang web Google.

# END