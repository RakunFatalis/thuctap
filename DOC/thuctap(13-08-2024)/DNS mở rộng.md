# DNS



# Mục lục

- [DNS](#dns)
- [Mục lục](#mục-lục)
- [I. DNS là gì, DNS hoạt động như thế nào,  phân loại DNS.](#i-dns-là-gì-dns-hoạt-động-như-thế-nào--phân-loại-dns)
  - [1. DNS là gì.](#1-dns-là-gì)
  - [2. DNS hoạt động như thế nào?](#2-dns-hoạt-động-như-thế-nào)
  - [3. Phân loại DNS.](#3-phân-loại-dns)
    - [a. DNS Master](#a-dns-master)
    - [b. DNS Slave](#b-dns-slave)
- [II. Cấu trúc cây DNS](#ii-cấu-trúc-cây-dns)
  - [Root Domain](#root-domain)
  - [Top-Level Domain (TLD)](#top-level-domain-tld)
  - [Second-Level Domains (SLDs)](#second-level-domains-slds)
  - [Subdomains](#subdomains)
  - [Hostnames](#hostnames)
- [III. Các loại bản ghi DNS trong zone file](#iii-các-loại-bản-ghi-dns-trong-zone-file)
- [IV. Cài đặt BIND](#iv-cài-đặt-bind)
- [V. Tìm hiểu một số lệnh dig, nslookup để query các record DNS](#v-tìm-hiểu-một-số-lệnh-dig-nslookup-để-query-các-record-dns)
  - [Bảng các lệnh dig](#bảng-các-lệnh-dig)
  - [Bảng các lệnh nslookup](#bảng-các-lệnh-nslookup)
- [VI. Bắt gói tin và phân tích khi truy vấn DNS](#vi-bắt-gói-tin-và-phân-tích-khi-truy-vấn-dns)
- [VII. DNS hoạt dộng ở layer nào trong mô hình OSI.](#vii-dns-hoạt-dộng-ở-layer-nào-trong-mô-hình-osi)
- [END.](#end)



# I. DNS là gì, DNS hoạt động như thế nào,  phân loại DNS.

## 1. DNS là gì.

Hệ thống phân giải tên miền (hay được viết tắt là DNS do tên tiếng Anh là Domain Name System) là một hệ thống cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền trên Internet.

DNS về căn bản là một hệ thống giúp cho việc chuyển đổi các tên miền mà con người dễ ghi nhớ (dạng ký tự, ví dụ www.example.com) sang địa chỉ IP vật lý (dạng số, ví dụ 123.11.5.19) tương ứng của tên miền đó. DNS giúp liên kết với các trang thiết bị mạng cho các mục đích định vị và địa chỉ hóa các thiết bị trên Internet.

Phép so sánh thường được sử dụng để giải thích cho DNS là, nó phục vụ như một "Danh bạ điện thoại", có khả năng tìm kiếm và dịch tên miền thành địa chỉ IP. Ví dụ, www.example.com dịch thành 208.77.188.166. Tên miền Internet dễ nhớ hơn các địa chỉ IP, là ``208.77.188.166`` (IPv4) hoặc ``2400:cb00:2048:1::c629:d7a2`` (IPv6).

Hệ thống phân giải tên miền phân phối trách nhiệm gán tên miền và lập bản đồ những tên tới địa chỉ IP bằng cách định rõ những máy chủ có thẩm quyền cho mỗi tên miền. Những máy chủ có tên thẩm quyền được phân công chịu trách nhiệm đối với tên miền riêng của họ, và lần lượt có thể chỉ định tên máy chủ khác độc quyền của họ cho các tên miền phụ. Kỹ thuật này đã thực hiện các cơ chế phân phối DNS, chịu đựng lỗi, và giúp tránh sự cần thiết cho một trung tâm đơn lẻ để đăng ký được tư vấn và liên tục cập nhật.

## 2. DNS hoạt động như thế nào?

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

## 3. Phân loại DNS.

### a. DNS Master

Khu vực DNS Master, hay còn gọi là khu vực DNS Primary, là nguồn gốc uy quyền cho các bản ghi DNS của một miền cụ thể. Trong khu vực DNS này lưu trữ các thông tin như địa chỉ IP, chi tiết máy chủ mail và các bản ghi liên quan đến miền. Khu vực DNS Master giữ bản sao gốc và có thể chỉnh sửa của các bản ghi này. 

Các quản trị viên chỉ có thể thực hiện các thay đổi và cập nhật cấu hình của miền trong khu vực DNS Master được lưu trữ trên máy chủ DNS Authoritative. Điều này giúp đảm bảo tính nhất quán và chính xác trong toàn bộ hệ thống DNS. Khu vực DNS Primary rất quan trọng trong việc duy trì kiểm soát thông tin DNS của miền, đảm bảo ánh xạ chính xác và cập nhật giữa tên miền và địa chỉ IP. 

Việc tập trung kiểm soát này cho phép quản lý các bản ghi DNS một cách hiệu quả và đơn giản hóa việc phân phối các thay đổi trong toàn bộ cơ sở hạ tầng DNS.

### b. DNS Slave

Khu vực DNS Slave, hay còn gọi lài khu vực DNS Secondary, là bản sao chỉ đọc của các bản ghi DNS. Điều này có nghĩa là các bản ghi DNS không thể được thêm trực tiếp vào khu vực DNS Secondary. Khu vực DNS Secondary chỉ có thể nhận các bản ghi được cập nhật từ khu vực Master của máy chủ DNS. Các bản ghi trong khu vực DNS Sao lưu chỉ có thể được quản lý tại máy chủ chính của bạn. Tính năng DNS Secondary có sẵn trong tất cả các gói trả phí của chúng tôi.

DNS hoạt động theo cách phân cấp, với nhiều máy chủ DNS chịu trách nhiệm phân giải tên miền. Khi người dùng cố gắng truy cập một trang web, thiết bị của họ sẽ gửi yêu cầu tới máy chủ DNS để lấy địa chỉ IP tương ứng. Trong cấu hình DNS tiêu chuẩn, bộ giải quyết DNS của người dùng thường sẽ liên hệ với máy chủ DNS chính liên kết với miền.

Trong trường hợp máy chủ DNS chính gặp sự cố hoặc không khả dụng, Khu vực DNS Secondary sẽ phát huy tác dụng. Khi được cấu hình đúng cách, Khu vực DNS Sao lưu cho phép máy chủ DNS phụ đảm nhiệm và cung cấp các bản ghi DNS cho miền. Điều này đảm bảo rằng ngay cả khi máy chủ DNS chính không thể truy cập, người dùng vẫn có thể truy cập trang web hoặc dịch vụ bằng cách phân giải tên miền thông qua máy chủ sao lưu.

# II. Cấu trúc cây DNS

Cấu trúc cây của DNS (Domain Name System) là một cấu trúc phân cấp, trong đó mỗi nút (node) đại diện cho một miền hoặc một phần của miền. Cấu trúc này giúp tổ chức và quản lý thông tin về tên miền theo một cách có hệ thống và hiệu quả.

![](/img/DNS_tree.png)

##  Root Domain

Root domain (Miền gốc) là đỉnh của cấu trúc cây DNS, được biểu thị bằng một dấu chấm "." nhưng thường không được viết ra khi sử dụng tên miền.

Có 13 hệ thống root server được đặt tên từ A đến M trên toàn cầu. Các máy chủ này không chứa bản ghi thông tin chi tiết của tất cả các tên miền mà chỉ lưu trữ thông tin về các TLD (Top-Level Domains).

![](/img/DNS_map_rootserver.png)

Khi một trình duyệt hoặc ứng dụng yêu cầu một tên miền, truy vấn DNS đầu tiên sẽ được gửi đến các máy chủ gốc.

## Top-Level Domain (TLD)

Tên miền cấp cao nhất (Top-level domain - TLD) là phần ngoài cùng bên phải của tên miền, nằm ngay sau dấu chấm cuối cùng. Còn được gọi là phần mở rộng tên miền, TLD được dùng để nhận biết các yếu tố nhất định của website, chẳng hạn như mục đích, chủ sở hữu hoặc khu vực địa lý.

Có 3 loại TLD thường gặp

* **Generic Top-Level Domain (gTLD)** là một trong các loại tên miền cấp cao nhất trong hệ thống phân loại tên miền của Internet. gTLD là các tên miền không liên quan đến một quốc gia cụ thể, mà mang tính chất tổng quát và thường được sử dụng cho các mục đích khác nhau. Dưới đây là những gTLD thường gặp:
    + **.com**: Dành cho các trang web thương mại.
    + **.org**: Dành cho các tổ chức phi lợi nhuận.
    + **.net**: Ban đầu dành cho các nhà cung cấp dịch vụ mạng, nhưng hiện nay có thể được sử dụng rộng rãi.
    + **.edu**: Dành cho các tổ chức giáo dục.

* **Sponsored Top-Level Domain (sTLD)** là một loại tên miền cấp cao nhất được quản lý bởi các tổ chức tài trợ, tức là các tổ chức đại diện cho một cộng đồng, ngành nghề, hoặc lĩnh vực cụ thể. Các tổ chức này có quyền kiểm soát và đặt ra các quy định về việc đăng ký và sử dụng các tên miền dưới sTLD của họ. Dưới đây là một số sTLD thường gặp

    + **.edu**: Dành cho các tổ chức giáo dục được công nhận.
    + **.aero**: Dành cho công nghiệp vận tải hàng không.
    + **.museum**: Dành cho các nhà bảo tàng
    + **.coop**: Dành cho các hợp tác xã

    Các sTLD thường có quy trình đăng ký nghiêm ngặt hơn so với các gTLD, vì chúng được thiết kế để phục vụ cho một nhóm người dùng cụ thể, và chỉ những đối tượng thuộc nhóm này mới có thể đăng ký tên miền dưới các sTLD.

* **Country code Top-Level Domain (ccTLD)**  là loại tên miền cấp cao nhất được phân bổ cho các quốc gia hoặc vùng lãnh thổ dựa trên mã quốc gia hai chữ cái theo tiêu chuẩn **ISO 3166-1 alpha-2**. Mỗi quốc gia hoặc vùng lãnh thổ có một ccTLD riêng, và chúng thường được sử dụng để chỉ ra rằng một trang web có liên quan đến một quốc gia cụ thể. Một só ccTLD thường gặp

    + **.vn**: Việt Nam
    + **.us**: Hoa Kỳ
    + **.uk**: Vương quốc Anh
    + **.jp**: Nhật Bản
    + **.de**: Đức
    + **.au**: Úc

    Một số ccTLD được sử dụng không chỉ trong phạm vi quốc gia mà còn trở nên phổ biến toàn cầu nhờ cách dễ nhớ hoặc liên quan đến các từ ngữ trong các ngôn ngữ khác, như:

    + **.tv**: Ban đầu là ccTLD của Tuvalu, nhưng hiện nay được sử dụng phổ biến cho các trang web liên quan đến truyền hình.
    + **.io**: Ban đầu là ccTLD của Lãnh thổ Ấn Độ Dương thuộc Anh, nhưng hiện được sử dụng rộng rãi trong ngành công nghệ thông tin.

##  Second-Level Domains (SLDs)

Đây là phần ngay trước TLD. Nó thường đại diện cho tên thương hiệu, tên công ty hoặc một từ khóa liên quan đến nội dung của trang web. Ví dụ, trong ``example.com``, ``example`` là SLD. SLD là phần mà người dùng có thể chọn khi đăng ký tên miền, và nó thường được sử dụng để xác định danh tính của trang web.

SLD thường là tên của công ty hoặc thương hiệu, giúp người dùng dễ dàng nhận diện và nhớ đến.

Trong cùng một TLD, các SLD phải là duy nhất. Ví dụ, ``example.com`` và ``anotherexample.com`` là hai tên miền hoàn toàn khác nhau, dù chúng cùng sử dụng TLD ``.com``.

## Subdomains

Subdomains là các tên miền con được tạo ra dưới một tên miền chính trong cấu trúc cây của DNS. Subdomains thường được sử dụng để tổ chức nội dung hoặc dịch vụ khác nhau trên một trang web. 

Một số ví dụ về subdomain:

  + ``mail.google.com``: Dùng để truy cập dịch vụ Gmail của Google, trong khi ``google.com`` là tên miền chính.
  
  + ``support.microsoft.com``: Dùng cho dịch vụ hỗ trợ khách hàng của Microsoft.

  + ``forum.example.com``: Được sử dụng cho diễn đàn hoặc cộng đồng người dùng trên trang example.com.

## Hostnames

Hostname là tên của một máy tính hoặc thiết bị trong một mạng. Đây là một phần quan trọng trong việc xác định và phân biệt các thiết bị trong mạng nội bộ hoặc trên Internet.

Hostname giúp các thiết bị trong một mạng xác định nhau. Trong mạng LAN của một tổ chức, mỗi máy tính có một hostname duy nhất. 

Khi bạn kết nối đến một máy tính qua mạng, bạn có thể sử dụng hostname thay vì địa chỉ IP. Ví dụ, thay vì gõ địa chỉ IP ``192.168.1.5``, bạn có thể gõ ``server1`` nếu đó là hostname của máy tính đó.

# III. Các loại bản ghi DNS trong zone file

Trong một zone file của hệ thống DNS, các bản ghi (record) cung cấp thông tin quan trọng về cách ánh xạ tên miền với các tài nguyên mạng. Dưới đây là các loại bản ghi phổ biến trong zone file:

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

# IV. Cài đặt BIND

BIND (Berkeley Internet Name Domain) là một phần mềm hệ thống máy chủ tên miền cơ bản và phổ biến nhất hiện nay. BIND được sử dụng trên hầu hết các máy chủ phân giải tên miền trên toàn thế giới.

Trong bài lab này mình có 2 máy ảo CentOS, một máy server và một máy client chúng có ip lần lượt là:

* **Server**: ``192.168.3.183/24``
* **Client**: ``192.168.3.111/24``

Trên cả 2 máy ảo ta đều cài đặt BIND, để cài đặt BIND ta sử dụng câu lệnh sau:

``# yum install bind -y``

![](/img/bind_install.png)

Khi các gói BIND của bạn được cài đặt, bạn cần khởi động dịch vụ của nó và cho phép nó tự khởi động sau mỗi lần khởi động lại, để bạn không phải bắt đầu thủ công mỗi lần. Chúng ta hãy chạy các lệnh sau để làm như vậy và sau đó kiểm tra trạng thái của dịch vụ BIND.

``# systemctl enable named``

``# systemctl start named``

``# systemctl status named``

![](/img/bind_status.png)

**Cấu hình BIND trên Server**

Cấu hình của BIND bao gồm nhiều tệp như tệp cấu hình chính và named.conf. Tên các tệp này bắt đầu bằng named vì đó là tên của tiến trình mà BIND chạy (với named được rút gọn từ “name daemon”, như trong “domain name daemon”). Bạn sẽ bắt đầu bằng cách cấu hình tệp named.conf

``# nano /etc/named.conf`` để chỉnh sửa file named.conf

![](/img/bind_blockoption.png)


**Cấu hình file BIND**

Bây giờ ta sẽ thêm các vùng chuyển tiếp và đảo ngược trong tệp ‘name.conf’ cho miền của chúng ta. Vì vậy, để thiết lập chỉnh sửa vùng chuyển tiếp /etc/named.conf theo cách như vậy để đặt các cấu hình sau.

``# nano /etc/named.conf``

Thêm hoặc chỉnh sửa các phần sau:

        options {
            directory "/var/named";
            allow-query { any; };
            listen-on port 53 { 192.168.0.183; };
            // Các cấu hình khác nếu cần
        };

        zone "local" IN {
            type master;
            file "local.zone";
        };

        zone "0.168.192.in-addr.arpa" IN {
            type master;
            file "0.168.192.in-addr.arpa.zone";
        };

**Tạo file zone cho domain:**

Tạo file zone chính tại ``/var/named/local.zone``:

``# nano /var/named/local.zone``

Thêm nội dung sau:

        $TTL 86400
        @   IN  SOA ns.hailong.info. admin.hailong.info. (
                    2024081901
                    3600
                    1800
                    1209600
                    86400 )

        @   IN  NS  ns.hailong.info.
        @   IN  A   192.168.0.183
        ns  IN  A   192.168.0.183

Tạo file zone ngược tại ``/var/named/0.168.192.in-addr.arpa.zone``:

``# nano /var/named/0.168.192.in-addr.arpa.zone``

Thêm nội dung sau:

        $TTL 86400
        @   IN  SOA  ns1.hailong.info. admin.hailong.info. (
                        2024081901 ; Serial
                        3600       ; Refresh
                        1800       ; Retry
                        1209600    ; Expire
                        86400 )    ; Minimum TTL
        ;
        @   IN  NS   ns1.hailong.info.
        @   IN  NS   ns2.hailong.info.
        ;
        183 IN  PTR  hailong.info.


**Kiểm tra lỗi file**

Kiểm tra file:

``# named-checkconf``

``# named-checkzone local /var/named/local.zone``

``# named-checkzone 0.168.192.in-addr.arpa /var/named/0.168.192.in-addr.arpa.zone``

**Khỏi động dịch vụ BIND**

``# systemctl start named``

``# systemctl enable named``

``# systemctl status named``

**Mở tường lửa nếu đang chặn cổng dịch vụ BIND**

``# firewall-cmd --zone=public --add-port=53/tcp --permanent``

``# firewall-cmd --zone=public --add-port=53/udp --permanent``

``# firewall-cmd --reload``

**Cấu hình file DNS trên máy client**

``# nano /etc/resolv.conf``

Thêm hoặc cập nhật dòng sau:

    nameserver 192.168.0.183


# V. Tìm hiểu một số lệnh dig, nslookup để query các record DNS

## Bảng các lệnh dig


| **Lệnh**| **Mô Tả**| **Ví Dụ**|
|----------------------------------|--------------------------------------------------------------|------------------------------------------|
| `dig example.com`| Truy vấn tất cả các bản ghi DNS cho tên miền.| `dig example.com`|
| `dig example.com A`| Truy vấn bản ghi A (Address Record) cho tên miền.| `dig example.com A`|
| `dig example.com MX`| Truy vấn bản ghi MX (Mail Exchange) cho tên miền.| `dig example.com MX`|
| `dig example.com NS`| Truy vấn bản ghi NS (Name Server) cho tên miền.| `dig example.com NS`|
| `dig -x 192.168.1.1`| Truy vấn bản ghi PTR (Pointer Record) cho địa chỉ IP.| `dig -x 192.168.1.1`|
| `dig example.com TXT`| Truy vấn bản ghi TXT (Text Record) cho tên miền.| `dig example.com TXT`|
| `dig example.com CNAME`| Truy vấn bản ghi CNAME (Canonical Name) cho tên miền.| `dig example.com CNAME`|
| `dig example.com SOA`| Truy vấn bản ghi SOA (Start of Authority) cho tên miền.| `dig example.com SOA`|
| `dig @8.8.8.8 example.com`| Truy vấn DNS từ máy chủ cụ thể.| `dig @8.8.8.8 example.com`|
| `dig example.com +noall +answer`| Hiển thị thông tin chi tiết, chỉ các bản ghi trả về.| `dig example.com +noall +answer`|
| `dig example.com +short`| Truy vấn DNS với định dạng ngắn gọn.| `dig example.com +short`|

Ví dụ: Mình sử dụng lệnh ``dig @192.168.0.183 -x 192.168.0.183`` để thực hiện truy vấn DNS ngược (reverse DNS lookup) từ máy chủ DNS có địa chỉ IP ``192.168.0.183`` và yêu cầu phân giải địa chỉ IP ``192.168.0.183`` về tên miền.

![](/img/dig_hailonginfo.png)

## Bảng các lệnh nslookup

| **Lệnh**| **Mô Tả**| **Ví Dụ**|
|-------------------------------|--------------------------------------------------------------|------------------------------------------|
| `nslookup example.com`| Truy vấn địa chỉ IP của tên miền.| `nslookup example.com`|
| `nslookup -query=MX example.com`| Truy vấn bản ghi MX (Mail Exchange) cho tên miền.| `nslookup -query=MX example.com`|
| `nslookup -query=NS example.com`| Truy vấn bản ghi NS (Name Server) cho tên miền.| `nslookup -query=NS example.com`|
| `nslookup -query=A example.com`| Truy vấn bản ghi A (Address Record) cho tên miền.| `nslookup -query=A example.com`|
| `nslookup 192.168.1.1`| Truy vấn bản ghi PTR (Pointer Record) cho địa chỉ IP.| `nslookup 192.168.1.1`|
| `nslookup example.com 8.8.8.8` | Chọn máy chủ DNS để thực hiện truy vấn.| `nslookup example.com 8.8.8.8`|
| `nslookup`| Sử dụng chế độ tương tác để thực hiện nhiều truy vấn.| `nslookup` (vào chế độ tương tác)|

**Ví dụ:** Lệnh nslookup ``hailong.info 192.168.0.183`` truy vấn máy chủ DNS tại địa chỉ ``192.168.0.183`` để tìm địa chỉ IP của tên miền ``hailong.info``. Kết quả cho thấy tên miền ``hailong.info`` được phân giải thành địa chỉ IP ``192.168.0.183``.

![](/img/nslookup_hailonginfo.png)

# VI. Bắt gói tin và phân tích khi truy vấn DNS

Để bắt gói tin trên cổng 53 (cổng mặc định của DNS) thì ta sử dụng lệnh ``tcpdump``. Nếu máy bạn chưa có thì cài đặt với lệnh sau:

``# yum update``

``#yum install tcpdump -y``

Thông thường khi bắt gói tin nó sẽ có dạng như sau:

![](/img/DNS_tcpdump.png)

Giờ ta hãy phân tích từng gói tin của DNS trên:

**Truy vấn DNS cho A Record (IPv4) của ``hailong.info``**

![](/img/DNS_tcpdump_A.png)

* **Gói tin 1**: ``192.168.0.111`` gửi một yêu cầu DNS đến máy chủ DNS tại ``localhost.localdomain`` để tra cứu bản ghi A (địa chỉ IPv4) của ``hailong.info``. Số hiệu truy vấn là ``26875``.

* **Gói tin 2**: Máy chủ DNS (localhost.localdomain) trả lời với bản ghi A cho hailong.info, có giá trị là ``192.168.0.183``. Truy vấn được đáp ứng với số hiệu ``26875`` và không có bản ghi phụ hoặc lỗi.

**Truy vấn DNS cho AAAA Record (IPv6) của hailong.info**

![](/img/DNS_tcpdump_AAAA.png)

* **Gói tin 3**: ``192.168.0.111`` gửi một yêu cầu DNS để tra cứu bản ghi AAAA (địa chỉ IPv6) của ``hailong.info``. Số hiệu truy vấn là ``1020``.

* **Gói tin 4**: Máy chủ DNS trả lời rằng không có bản ghi AAAA cho ``hailong.info``, do đó số bản ghi trong phần trả lời là ``0``.

**Truy vấn DNS ngược (PTR Record) cho địa chỉ IPv4 192.168.0.183**

![](/img/DNS_tcpdump_PTR.png)

* **Gói tin 5**: Máy chủ DNS (localhost.localdomain) gửi yêu cầu để tra cứu bản ghi PTR cho địa chỉ IPv4 ``192.168.0.183`` (được chuyển đổi thành 183.0.168.192.in-addr.arpa). Số hiệu truy vấn là ``61418``.

* **Gói tin 6**: Máy chủ DNS trả lời với mã lỗi ``NXDomain``, nghĩa là không có bản ghi PTR cho địa chỉ 192.168.0.183.

# VII. DNS hoạt dộng ở layer nào trong mô hình OSI.

DNS (Domain Name System) hoạt động chủ yếu ở Layer 7 của mô hình OSI, tức là Application Layer. Lí do nó hoạt động ở layer 7.

1. **Chức Năng Ứng Dụng**

    DNS cung cấp dịch vụ phân giải tên miền thành địa chỉ IP và ngược lại, điều này liên quan đến các dịch vụ và ứng dụng cụ thể mà người dùng hoặc các ứng dụng mạng sử dụng. Đây là nhiệm vụ của Application Layer, nơi các giao thức mạng cấp cao hoạt động để cung cấp các dịch vụ ứng dụng cho người dùng.

2. **Giao Thức Cấp Cao**

    Giao thức DNS là giao thức cấp cao được sử dụng để tìm kiếm và phân giải các tên miền. Giao thức này sử dụng UDP và TCP trên Layer 4 (Transport Layer) để truyền tải dữ liệu, nhưng logic phân giải tên miền và các quy trình xử lý thuộc về Application Layer.

3. **Dịch Vụ Tên Miền:**

    DNS không chỉ là một giao thức truyền dữ liệu mà còn là một dịch vụ hỗ trợ ứng dụng, giúp các ứng dụng web, email, và các dịch vụ khác hoạt động bằng cách chuyển đổi các tên miền dễ nhớ thành địa chỉ IP mà các máy chủ và thiết bị mạng có thể hiểu.

**Tổng kết lại:** DNS nằm ở Layer 7 vì nó cung cấp dịch vụ phân giải tên miền cho các ứng dụng và người dùng cuối. Mặc dù DNS sử dụng các giao thức ở Layer 4 (như UDP và TCP) để truyền tải dữ liệu, toàn bộ quá trình xử lý và dịch vụ phân giải tên miền được thực hiện ở Layer 7, nơi các dịch vụ ứng dụng mạng được cung cấp.

# END. 
