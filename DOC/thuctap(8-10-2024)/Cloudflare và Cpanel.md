# Cloudflare và CPanel


# Mục lục

- [Cloudflare và CPanel](#cloudflare-và-cpanel)
- [Mục lục](#mục-lục)
- [I. Tạo tài khoản CloudFlare, trỏ tên miền về CloudFlare và trỏ IP host](#i-tạo-tài-khoản-cloudflare-trỏ-tên-miền-về-cloudflare-và-trỏ-ip-host)
  - [1. Tạo tài khoản CloudF\\lare](#1-tạo-tài-khoản-cloudflare)
  - [2.Trỏ tên miền về CloudFlare](#2trỏ-tên-miền-về-cloudflare)
  - [3. Trỏ IP host](#3-trỏ-ip-host)
- [II. cPanel](#ii-cpanel)
  - [1. cPanel là gì?](#1-cpanel-là-gì)
  - [2. Giao diện của cPanel.](#2-giao-diện-của-cpanel)
  - [3. Các chức năng của cPanel.](#3-các-chức-năng-của-cpanel)
- [III. Cài đặt website trên cPanel](#iii-cài-đặt-website-trên-cpanel)
  - [1. Cài đặt thủ công](#1-cài-đặt-thủ-công)
  - [2. Cài đặt thông qua Softaculous App Installer](#2-cài-đặt-thông-qua-softaculous-app-installer)
  - [3. Cài đặt thông qua Git™ Version Control](#3-cài-đặt-thông-qua-git-version-control)
- [END](#end)

# I. Tạo tài khoản CloudFlare, trỏ tên miền về CloudFlare và trỏ IP host

## 1. Tạo tài khoản CloudF\lare
Các bạn vào trang chủ của Cloudflare để tạo một tài khoản: https://www.cloudflare.com/

Các bạn nhấn vào ô Sign Up để tiến hành vào trang đăng ký tài khoản.

![](/img/Cloude_Sign_Up.png)

Tại đây các bạn điền đẩy đủ thông tin email và mật khẩu cho tài khoản đăng ký của các bạn

![](/img/Cloude_Sign_Up_Process.png)

## 2.Trỏ tên miền về CloudFlare

Sau khi các bạn dăng kí xong thì các bạn sẽ được chuyển tới trang "**Add site**" của Cloudflare, tại đây bạn nhập tên miền hiện có của mình để bắt đầu kết nối với Cloudflare.

![](/img/Cloude_Addsite.png)

Khi các bạn đã thêm tên miền thì trang sẽ chuyển hướng các bạn tới trang **lựa chọn gói dịch vụ** của CloudFlare.

![](/img/Cloude_Service.png)

Tại đây, bạn có thể chọn giữa các gói dịch vụ khác nhau dựa trên nhu cầu của website:

* **Free**: Gói miễn phí với các tính năng cơ bản, bao gồm bảo vệ chống DDoS, SSL miễn phí và hạn chế dựa trên địa chỉ IP.

* **Pro**: **$20/tháng**, bổ sung các tính năng như bảo vệ nâng cao với WAF, cache thông minh cho WordPress, tối ưu hóa hình ảnh tự động.

* **Business**: **$200/tháng**, hỗ trợ chứng chỉ SSL tùy chỉnh, chống mã độc từ bên thứ ba, uptime 100% và nhiều tính năng bảo mật.

* **Enterprise**: Tùy chỉnh giá, dành cho các doanh nghiệp lớn với các tính năng bảo mật tiên tiến nhất, API Gateway, quản lý bot và hỗ trợ cấp cao.

Khi các bạn đã thêm domain của các bạn vào Cloudflare thì trang sẽ thông báo domain của bạn chưa được kích hoạt vì domain của bạn chưa được cập nhật nameserver do cloudflare cung cấp. Các bạn cần thay đổi nameserver tại các nhà dịch vụ cung cấp tên miền bằng nameserver do cloudflare cung cấp.

Cloudeflare sẽ cung cấp cho các bạn 2 nameserver tạo ngẫu nhiên, các bạn chỉ cần thay hoặc thêm 2 nameserver này vào các danh sách nameserver tại nơi cung cấp tên mièn của bạn. Các nhà cung cấp tên miền sẽ cần mất đến 24 giờ để xử lý các thay đổi về nameservers mà bạn đã thực hiện. Tuy nhiên, trong nhiều trường hợp, quá trình này có thể hoàn tất nhanh hơn.

Khi tên miền của các bạn đã được kích hoạt trên Cloudflare, các bạn sẽ nhận được thông báo qua email từ Cloudflare.

![](/img/Cloude_Domain_NotActive.png)

## 3. Trỏ IP host

Để trỏ IP host đến tên miền của mình, bên trong mục Dashboard các bạn vào mục **DNS** -> **Records**. Sau khi các bạn vào được trang **Records**, bạn nhấp chuột vào ô **Add record**

![](/img/Cloude_Records.png)

Tại đây các bạn sẽ có các thông tin sau:

  * **Type (Loại)**: là nơi bạn chọn loại bản ghi DNS mà bạn muốn tạo.

  * **Name (Tên)**: Đây là nơi bạn xác định tên miền hoặc subdomain mà bản ghi DNS sẽ áp dụng. Dấu @ thể hiện bản ghi này sẽ được dùng cho tên miền gốc (root domain).

  * **IPv4 address**: Bạn cần điền địa chỉ IP của máy chủ mà tên miền sẽ trỏ tới. Đây là địa chỉ máy chủ chạy trang web của bạn.

  * **Proxy status (Trạng thái proxy)**: Khi bật (màu cam với biểu tượng đám mây), Cloudflare sẽ che giấu địa chỉ IP thực và hoạt động như một proxy bảo vệ. Nếu tắt (màu xám), Cloudflare sẽ chỉ cung cấp dịch vụ DNS mà không có tính năng bảo mật proxy.

  * **TTL (Time to Live)**: Thiết lập thời gian tồn tại của bản ghi DNS trước khi nó cần được cập nhật lại trên máy chủ DNS khác. "Auto" cho phép Cloudflare tự động quản lý TTL cho bạn.

Sau khi các bạn đã xác định record của mình là gì thì các bạn nhấn vào ô **Save** để lưu lại.

# II. cPanel

## 1. cPanel là gì?

Theo Wikipedia, cPanel là phần mềm quản lý hosting web được phát triển bởi cPanel, L.L.C. Nó cung cấp một giao diện đồ họa (GUI) và các công cụ tự động hóa được thiết kế để đơn giản hóa quá trình quản lý website cho người sở hữu trang web hoặc "người dùng cuối". cPanel cho phép quản lý thông qua một trình duyệt web tiêu chuẩn với cấu trúc ba tầng. Trong khi cPanel bị giới hạn ở việc quản lý một tài khoản hosting duy nhất, cPanel & WHM cho phép quản lý toàn bộ máy chủ.

Ngoài giao diện đồ họa, cPanel còn có quyền truy cập dòng lệnh và API, cho phép các nhà cung cấp phần mềm bên thứ ba, các tổ chức web hosting và các nhà phát triển tự động hóa các quy trình quản trị hệ thống tiêu chuẩn. cPanel & WHM được thiết kế để hoạt động như một máy chủ chuyên dụng hoặc máy chủ ảo (VPS). Phiên bản cPanel & WHM mới nhất hỗ trợ cài đặt trên AlmaLinux, Rocky Linux, CloudLinux OS và Ubuntu.

## 2. Giao diện của cPanel.

Giao diện của cPanel có 6 phần chính:

* **1. Thanh điều hướng:**

  Đây là phần trên cùng của giao diện cPanel, cung cấp truy cập nhanh đến các chức năng quan trọng:

  ![](/img/cPanel_NavigationBar.png)

* **2. Menu chính:**

  Menu chính cho phép bạn điều hướng đến trang Tools Page từ bất kỳ giao diện nào. Menu chính trong cPanel có thể tùy chỉnh tùy thuộc vào nhà cung cấp dịch vụ hosting. Mỗi nhà cung cấp có thể cài đặt cPanel theo cách riêng của họ và tùy chỉnh các tính năng hoặc module xuất hiện trong giao diện của cPanel để phù hợp với nhu cầu của khách hàng.

  ![](/img/cPanel_MainMenu.png)

* **3. Trang công cụ**

  Trang công cụ của cPanel là nơi tập trung các công cụ và tính năng quản lý hosting được sắp xếp theo từng danh mục cụ thể. Đây là trang chính mà người dùng thường truy cập để thực hiện các tác vụ quản lý website, tài khoản email, tên miền, và cơ sở dữ liệu.

  ![](/img/cPanel_ToolPage.png)

* **4. Tính năng**

  Đây là tập hợp các công cụ cụ thể mà cPanel cung cấp cho việc quản lý website và hosting. Từ việc quản lý tệp tin, email, cơ sở dữ liệu đến các công cụ bảo mật, quản trị viên có thể thao tác trực tiếp thông qua giao diện đồ họa.

  ![](/img/cPanel_Features.png)

* **5. Thông tin chung (General Information):**

  Thông tin chung (General Information) trong cPanel cung cấp cái nhìn tổng quan về tài khoản hosting và tình trạng hệ thống. Phần này thường nằm ở cột bên phải hoặc trên cùng của giao diện, tùy thuộc vào giao diện cPanel mà nhà cung cấp hosting tùy chỉnh.

  ![](/img/cPanel_General_Information.png)

* **6. Thống kê (Statistics)**

  Phần Thống kê (Statistics) trong cPanel cung cấp một cái nhìn tổng quan nhanh về việc sử dụng tài nguyên của tài khoản hosting, giúp người dùng theo dõi hiệu suất và đảm bảo họ không vượt quá các giới hạn được đặt ra bởi gói dịch vụ hosting của họ. Đây là một phần quan trọng vì nó cho phép người dùng kiểm soát tài nguyên mà website của họ tiêu thụ.

  ![](/img/cPanel_Statistics.png)

## 3. Các chức năng của cPanel.

Trong phần công cụ (Tools) trong cPanel có nhiều mục khác nhau, tùy thuộc vào nhà cung cấp hosting và cấu hình của cPanel mà bạn sử dụng. Thông thường các trang Tools trong cPanel sẽ bao gồm các nhóm công cụ chính sau đây:

* **Email**

  Trong cPanel, phần Email (Quản lý email) cung cấp các công cụ để quản lý tài khoản email, cấu hình và kiểm soát các tính năng liên quan đến email.

  ![](/img/cPanel_Features_Email.png)

  Một số công cụ thường được dùng trong phần Email này:

  + **Email Accounts (Tài khoản email)**: Tạo và quản lý tài khoản email.
  
  + **Forwarders (Chuyển tiếp email)**: Chuyển tiếp email từ một địa chỉ sang địa chỉ khác.
  
  + **Autoresponders (Trả lời tự động)**: Thiết lập trả lời email tự động.
  
  + **Email Filters (Lọc email)**: Cài đặt các quy tắc lọc email.
  
  + **Spam Filters (Lọc thư rác)**: Quản lý và cấu hình lọc thư rác.


* **Files**

  Trong cPanel, mục Files thường chứa nhiều công cụ và tùy chọn để quản lý các tập tin trên máy chủ của bạn.

  ![](/img/cPanel_Features_Files.png)

  Một số công cụ trong phần Files thường được sử dụng:

  + **File Manager (Trình quản lý tập tin)**: Công cụ này cho phép bạn duyệt, tải lên, tải xuống, sửa đổi và xóa các tập tin và thư mục trên máy chủ. Bạn có thể sử dụng nó để quản lý các tệp web, hình ảnh và các tài liệu khác.

  + **FTP Accounts (Tài khoản FTP)**: Tại đây, bạn có thể tạo và quản lý các tài khoản FTP để truy cập vào các tập tin trên máy chủ. Bạn có thể đặt quyền truy cập cho từng tài khoản và thiết lập các thư mục gốc cho chúng.

  + **Backup (Sao lưu)**: Phần này cho phép bạn tạo sao lưu cho tài khoản cPanel của mình, bao gồm cả các tệp và cơ sở dữ liệu. Bạn cũng có thể tải xuống các bản sao lưu mà bạn đã tạo trước đó.

  + **Disk Usage (Dung lượng đĩa)**: Tại đây, bạn có thể xem mức sử dụng đĩa của từng thư mục trên tài khoản của bạn, giúp bạn theo dõi không gian lưu trữ mà bạn đã sử dụng.

  + **Web Disk**: Tính năng này cho phép bạn truy cập và quản lý các tệp trên máy chủ như một ổ đĩa cục bộ. Bạn có thể kết nối Web Disk với máy tính của mình để dễ dàng truy cập các tệp từ máy tính của bạn.

* **Databases**

  Trong cPanel, mục Databases cung cấp các công cụ để quản lý cơ sở dữ liệu trên máy chủ của bạn.

  ![](/img/cPanel_Features_Databases.png)

  + **phpMyAdmin**: Đây là công cụ phổ biến nhất để quản lý cơ sở dữ liệu MySQL. Bạn có thể sử dụng phpMyAdmin để tạo, sửa đổi, xóa cơ sở dữ liệu và bảng, cũng như thực hiện các truy vấn SQL.

  + **Manage My Databases**: Công cụ giúp bạn quản lí các cơ sở dữ liệu của bạn một cách tổng quát hơn

  + **Database Wizard**:  Tính năng này thường được sử dụng để đơn giản hóa quá trình tạo cơ sở dữ liệu mới và người dùng. Nó hướng dẫn bạn qua các bước cần thiết để thiết lập một cơ sở dữ liệu mới, bao gồm việc định nghĩa tên cơ sở dữ liệu, người dùng và quyền truy cập.

  + **Remote Database Access**: Cho phép các ứng dụng hoặc máy chủ bên ngoài kết nối với cơ sở dữ liệu của bạn từ xa, bao gồm cấu hình địa chỉ IP và quyền truy cập.

* **Doamins**

  Phần Domains trong cPanel là khu vực quản lý các tên miền mà bạn sở hữu.

  ![](/img/cPanel_Features_Domains.png)

  Một số công cụ phổ biến trong phần Domains này:

  + **Site Publisher**: Công cụ giúp bạn tạo nhanh một trang web đơn giản (mẫu trang sẵn có) mà không cần kiến thức về lập trình.

  + **Domains**: Quản lý các tên miền được liên kết với tài khoản cPanel của bạn. Bạn có thể thêm, xóa, hoặc thay đổi cấu hình tên miền tại đây.

  + **Redirects**: Cho phép bạn chuyển hướng một trang web hoặc URL sang một trang web khác. Ví dụ, bạn có thể chuyển hướng tên miền chính của mình sang một tên miền khác hoặc một thư mục con.

  + **Zone Editor**: Quản lý bản ghi DNS của tên miền. Tại đây, bạn có thể thêm, chỉnh sửa hoặc xóa các bản ghi như A, CNAME, MX, TXT... để kiểm soát cách mà tên miền của bạn trỏ đến các dịch vụ như máy chủ web, email...

  + **Dynamic DNS**: Công cụ này cho phép bạn thiết lập hệ thống Dynamic DNS (DNS động), nơi mà bạn có thể cập nhật địa chỉ IP cho tên miền của mình một cách tự động.

* **Metris**

  Phần Metrics trong cPanel cung cấp các công cụ giúp bạn theo dõi và phân tích hoạt động của website, từ đó tối ưu hóa và cải thiện trải nghiệm người dùng.

  ![](/img/cPanel_Features_Metrics.png)

  Một số công cụ phổ biến trong Metrics:

  + **Visitors**: Hiển thị thông tin chi tiết về những người truy cập vào website của bạn, bao gồm địa chỉ IP, ngày giờ, và số lần truy cập.

  + **Errors:** Hiển thị các lỗi xảy ra trên website của bạn, chẳng hạn như lỗi 404 (trang không tìm thấy) hoặc lỗi 500 (lỗi máy chủ).

  + **Bandwidth**: Theo dõi lưu lượng truy cập sử dụng trên website, giúp bạn biết lượng dữ liệu đã truyền tải trong các khoảng thời gian nhất định.

  + **Raw Access**: Cung cấp quyền truy cập vào các file log thô của máy chủ, cho phép bạn tải về các file chứa dữ liệu về tất cả các yêu cầu đến website của bạn.

* **Security**

  Phần Security trong cPanel cung cấp các công cụ bảo mật để bảo vệ website và máy chủ của bạn khỏi các mối đe dọa tiềm ẩn và giữ an toàn cho dữ liệu và thông tin của bạn.

  ![](/img/cPanel_Features_Security.png)

  Một số công cụ phổ biến trong mục Security:

  + **SSH Access**: Cung cấp quyền truy cập an toàn vào máy chủ qua SSH (Secure Shell), cho phép bạn thực hiện các lệnh trực tiếp trên máy chủ.

  + **IP Blocker**: Cho phép bạn chặn các địa chỉ IP cụ thể hoặc một dải địa chỉ IP không mong muốn truy cập vào website của bạn.

  + **SSL/TLS**: Quản lý các chứng chỉ SSL/TLS để mã hóa dữ liệu giữa trình duyệt và máy chủ, giúp bảo mật thông tin người dùng và dữ liệu truyền tải.

  + **SSL/TLS Status**: Hiển thị trạng thái hiện tại của các chứng chỉ SSL/TLS trên website của bạn, cho biết chứng chỉ có hợp lệ và hoạt động chính xác hay không.

  + **Two-Factor Authentication**: Thêm một lớp bảo mật cho tài khoản cPanel của bạn bằng cách yêu cầu mã xác thực thứ hai (thường là từ một ứng dụng trên điện thoại) khi đăng nhập.  

* **Software**
  Phần Software trong cPanel cung cấp các công cụ liên quan đến việc quản lý phần mềm và ứng dụng chạy trên máy chủ của bạn. Đây là nơi bạn có thể cài đặt và quản lý các ứng dụng, cũng như cấu hình môi trường lập trình.

  ![](/img/cPanel_Features_Software.png)

  Một số công cụ được dùng phổ biến trong mục Software:

  + **Optimize Website**: Công cụ tối ưu hóa hiệu suất website của bạn bằng cách nén nội dung (ví dụ: HTML, CSS, JavaScript) để giảm kích thước tệp truyền qua mạng và tăng tốc thời gian tải trang.

  + **MultiPHP Manager**: Cho phép bạn chọn và quản lý phiên bản PHP mà bạn muốn sử dụng cho các website của mình, cũng như cấu hình các tùy chọn PHP.
  
  + **Wordpress Manager by Softaculous**: một công cụ quản lý WordPress được tích hợp trong cPanel, giúp bạn dễ dàng cài đặt, quản lý, và tối ưu hóa website WordPress mà không cần phải thực hiện thủ công.
  
  + **Select PHP Version**: công cụ giúp bạn chọn và thay đổi phiên bản PHP mà website của bạn sử dụng. Bạn có thể chọn phiên bản PHP phù hợp với mã nguồn và yêu cầu của các ứng dụng web mà bạn đang chạy.

* **Advanced**
  
  Mục Advanced cung cấp các công cụ và tính năng nâng cao dành cho người quản trị web để quản lý các tác vụ kỹ thuật phức tạp hơn. Các công cụ trong mục Advanced thường hỗ trợ quản lý website và server ở mức độ sâu hơn, bao gồm các cài đặt hệ thống, cron jobs, quản lý mã nguồn, và các tính năng liên quan đến bảo mật và tối ưu hóa.

  ![](/img/cPanel_Features_Advanced.png)

  Một số công cụ được dùng phổ biến trong mục Advanced:

  + **Cron Jobs**: Cho phép bạn lập lịch các tác vụ tự động để chúng được thực hiện theo thời gian định trước. Đây là công cụ rất hữu ích để tự động hóa các tác vụ như gửi email, tạo báo cáo, hoặc chạy các script cụ thể.

  + **Track DNS**: Giúp bạn theo dõi và kiểm tra các bản ghi DNS của tên miền. Bạn có thể kiểm tra trạng thái DNS của miền và xác minh tính chính xác của các bản ghi (A, CNAME, MX, TXT, v.v.).

  + **Terminal**: Truy cập trực tiếp vào dòng lệnh của server từ giao diện cPanel. Đây là tính năng dành cho người dùng nâng cao muốn sử dụng các lệnh Linux để quản lý server một cách linh hoạt và mạnh mẽ hơn.

  + **Error Pages**: Tùy chỉnh các trang lỗi như 404 (không tìm thấy trang), 500 (lỗi server), v.v. Bạn có thể tạo các trang lỗi cá nhân hóa để hiển thị thông tin thân thiện hơn với người dùng khi gặp lỗi.

  + **Redis**: Được tích hợp để tăng tốc độ và hiệu suất của các ứng dụng web bằng cách sử dụng nó như một cache hoặc một datastore. Tùy vào dịch vụ hosting mà bạn đang sử dụng, Redis có thể được kích hoạt hoặc cấu hình từ giao diện cPanel.

* **Preferences**

  Trong cPanel, mục Preferences thường chứa các tùy chọn cấu hình cá nhân và cài đặt liên quan đến tài khoản người dùng.

  ![](/img/cPanel_Features_Preferences.png)

  + **Change Language**: Tùy chọn để thay đổi ngôn ngữ giao diện cPanel. Người dùng có thể chọn ngôn ngữ mà họ muốn sử dụng trong quá trình quản lý tài khoản.

  + **User Manager**: Một tính năng hữu ích trong cPanel cho phép bạn quản lý các subaccount (tài khoản phụ) trong tài khoản hosting của mình.

  + **Password & Security**: Cho phép bạn quản lý các khía cạnh bảo mật của tài khoản, chủ yếu liên quan đến việc thay đổi mật khẩu và thiết lập các biện pháp bảo mật bổ sung. 

  + **Contact Information**: Có thể thiết lập và quản lý thông tin liên hệ cho tài khoản của mình. Điều này rất quan trọng để đảm bảo rằng bạn nhận được thông báo và cập nhật liên quan đến tài khoản hosting của mình.

* **Softaculous App Installer**

  Softaculous là một công cụ tiện ích tích hợp trong cPanel, cho phép bạn dễ dàng cài đặt và quản lý các ứng dụng web phổ biến chỉ với vài cú nhấp chuột. Đây là một giải pháp tuyệt vời cho những người không có nhiều kinh nghiệm kỹ thuật nhưng vẫn muốn phát triển trang web của mình.

  ![](/img/cPanel_Features_SoftaculousAppInstaller.png)

# III. Cài đặt website trên cPanel

Có nhiều cách để các bạn có thể cài đặt website lên trên cPanel, tại đây mình sẽ hướng dẫn những cách phổ biến mà mọi người thường dùng nhất

## 1. Cài đặt thủ công

Đây là phương pháp phổ biến và cơ bản, phù hợp cho những người thích làm mọi thứ từ đầu hoặc cần kiểm soát hoàn toàn quá trình cài đặt.

* **Bước 1. Đăng nhập vào cPanel**

  Để đăng nhập vào trang cPanel của các bạn, các bạn cần thông qua đường dẫn:

  **http://yourdomain.com/cpanel**

  Hoặc thông qua port 2083:

  **http://yourdomain.com:2083**

  Các bạn nhớ thay **yourdomain.com** bằng các domain của các bạn.

  ![](/img/cPanel_LoginPage.png)

* **Bước 2. Mở File Manager**

  Một khi các bạn đã vào được trang cPanel, các bạn tìm tới mục ''**Files**'' và tìm tới **File Manager** 

  ![](/img/cPanel_FileManager.png)

* **Bước 3: Điều hướng đến thư mục Public**

  Trong **File Manager**, điều hướng đến thư mục **public_html**. Đây là thư mục nơi các tệp website của bạn nên được lưu trữ.

  ![](/img/cPanel_public_html.png)

* **Bước 4: Tải các tệp website lên**

  Sau khi các bạn đã trong thư mục ''**public_html**'' các bạn nhấn vào ô ''**Upload**'' để vào trang file upload

  ![](/img/cPanel_public_html_upload.png)

  ![](/img/cPanel_Upload_Page.png)

  Để tránh mất thời gian upload từng file lên thì các bạn đóng gói các file webiste của bạn thành tệp zip xong rồi tải lên trên cPanel và unzip nó ra trong thư mục ''**public_html**''.

  ![](/img/cPanel_Select_file.png)

  Đây là trong thư mục "**public_html**" sau khi đã upload mã nguồn thành công

  ![](/img/cPanel_Upload_Success.png)

  Các bạn vào tên miền của các bạn để kiểm tra xem website đã upload thành công chưa.

## 2. Cài đặt thông qua Softaculous App Installer

Cài đặt website thông qua Softaculous App Installer trên cPanel phù hợp với những ai muốn cài đặt nhanh chóng mà không cần kỹ năng kỹ thuật phức tạp. Quá trình này tự động và dễ sử dụng, giúp tiết kiệm thời gian và đơn giản hóa việc triển khai trang web. Tuỳ vào nhà cung cập dịch vụ sẽ có Softaculous App Installer khác nhau nhưng phổ biến nhất và nhiều người nhất hiện nay là Wordpress.

* **Bước 1. Đăng nhập vào cPanel**

  Để đăng nhập vào trang cPanel của các bạn, các bạn cần thông qua đường dẫn:

  **http://yourdomain/cpanel**

  Hoặc thông qua port 2083:

  **http://yourdomain:2083**

  Các bạn nhớ thay **yourdomain** bằng các domain của các bạn.

  ![](/img/cPanel_LoginPage.png)

* **Bước 2. Truy cập vào trang cài đặt Wordpress**

Các bạn tìm đến mục Software mà kiếm cho mình phần **Softaculous App Installer** tại đây của mình là **WordPress Manager by Softaculous** và click chuột vào phần đó để vào trang cài đặt Wordpress

  ![](/img/cPanel_Softaculos.png)

* **Bước 3. Cài đặt Wordpress**

  Sau khi đã vào trang cài đặt các bạn click vào ô "**Install**" để bắt đầu thực hiện quá trình cài đặt Wordpress

  ![](/img/cPanel_Softaculos_WebInstall.png)

  ![](/img/cPanel_Wordpress_Install.png)

  Tại đây sẽ có vài mục các bạn cần lưu ý:

  * Mục **Software Setup**, nơi bạn có thể cấu hình cài đặt cơ bản cho WordPress:

    + **Choose Installation URL**: Đây là nơi bạn chọn giao thức (HTTP hoặc HTTPS) và tên miền mà bạn muốn cài đặt WordPress lên.

    + **Choose Protocol**: Chọn giữa http:// hoặc https:// dựa trên việc tên miền của bạn có hỗ trợ SSL hay không (nếu đã cài SSL, bạn nên chọn https://).

    + **Choose Domain**: Chọn tên miền mà bạn muốn cài đặt WordPress.

    + **In Directory**: Mục này dùng để nhập tên thư mục nếu bạn muốn cài đặt WordPress trong một thư mục con (ví dụ: https://yourdomain.com/blog). Nếu để trống, WordPress sẽ được cài đặt trực tiếp ở thư mục gốc của tên miền.

    + **Choose the version you want to install**: Chọn phiên bản Wordpress mà bạn muốn cài đặt.

    ![](/img/cPanel_SoftwareSetup.png)

  * Mục **Site Setting**, nơi bạn cấu hình tên, mô tả và một số tính năng cơ bản cho trang web WordPress của bạn:
    + **Site Name**: Đây là tên trang web của bạn. Tên này sẽ hiển thị trên tiêu đề của trình duyệt và trong phần đầu trang của trang web. Bạn có thể đặt tên theo sở thích hoặc theo chủ đề của trang web.
    
    + **Site Description**: Đây là mô tả ngắn gọn về trang web của bạn. Mô tả này giúp người dùng hiểu rõ hơn về nội dung và mục đích của trang web. Nó cũng có thể được hiển thị trong các kết quả tìm kiếm.

    + **Enable Multisite (WPMU)**: Đây là tùy chọn cho phép bạn kích hoạt tính năng WordPress Multisite. Nếu được bật, bạn có thể quản lý nhiều trang web từ một cài đặt WordPress duy nhất. Tính năng này thường được sử dụng cho các mạng lưới blog hoặc các tổ chức lớn có nhiều trang web con. Nếu bạn không có nhu cầu quản lý nhiều trang web, bạn có thể để tùy chọn này tắt.

    + **Disable WordPress Cron**: Tùy chọn này cho phép bạn tắt chức năng Cron của WordPress, là một hệ thống để lập lịch thực hiện các tác vụ tự động (như tự động lưu bản nháp, gửi email thông báo, và cập nhật plugin). Nếu bạn tắt tùy chọn này, bạn sẽ cần quản lý cron jobs bằng cách khác (ví dụ: sử dụng cron trên server). Tùy chọn này thường không cần thiết cho người dùng bình thường và nên để ở trạng thái tắt trừ khi bạn có lý do cụ thể để bật.

    ![](/img/cPanel_SiteSettings.png)

  * Mục **Admin Account**, nơi bạn cài đặt tài khoản và mật khẩu quản trị của Wordpress:

    + **Admin Username**: Đây là tên đăng nhập của tài khoản quản trị viên WordPress. Bạn nên chọn một tên duy nhất và không dễ đoán để tăng cường bảo mật. Tránh sử dụng các tên mặc định như "admin" để giảm thiểu rủi ro bị tấn công.

    + **Admin Password**: Đây là mật khẩu cho tài khoản quản trị viên. Mật khẩu nên đủ mạnh, kết hợp giữa chữ hoa, chữ thường, số và ký tự đặc biệt. Softaculous sẽ hiển thị chỉ số độ mạnh của mật khẩu (Strength Indicator) để bạn biết mật khẩu của mình có an toàn hay không. Cố gắng đạt điểm số cao để đảm bảo bảo mật. Hoặc, bạn có thể click vào biểu tượng chìa khoá để tạo mật khẩu ngẫu nhiên có độ bảo mật cao.

    + **Strength Indicator (0/100)**: Đây là một chỉ số cho biết độ mạnh của mật khẩu bạn đã nhập. Điểm số từ 0 đến 100 cho thấy mức độ an toàn của mật khẩu; mật khẩu càng mạnh, điểm số càng cao. Hãy chắc chắn rằng mật khẩu có điểm số cao để bảo vệ tài khoản của bạn.

    + **Admin Email**: Đây là địa chỉ email của tài khoản quản trị viên. Email này sẽ được sử dụng để gửi thông báo, khôi phục mật khẩu, và nhận các thông báo quan trọng từ WordPress. Hãy chắc chắn rằng đây là một địa chỉ email chính xác mà bạn có quyền truy cập.

    ![](/img/cPanel_AdminAccount.png)

  * Mục **Choose Language**, nơi bạn chọn ngôn ngữ hiển thị cho trang Wordpress

    ![](/img/cPanel_ChooseLanguage.png)

  * Mục **Select Plugin(s)**, nơi bạn có thể chọn các plugin bổ sung cho trang web của mình. Nếu bạn không chắc chắn về một plugin nào đó, bạn có thể bỏ qua nó và cài đặt sau khi trang web đã hoạt động.

    ![](/img/cPanel_Select%20Plugin(s).png)
  
  * Phần **Advanced Options**, tùy chọn trong phần này giúp bạn cấu hình cơ sở dữ liệu, tiền tố bảng, và các cài đặt nâng cấp tự động cho WordPress, cũng như quản lý thông báo và vị trí sao lưu. Nếu bạn không muốn thay đổi tên cơ sở dữ liệu, tiền tố bảng, hay cấu hình các tùy chọn nâng cấp và sao lưu, bạn có thể để các trường này ở mặc định.

    ![](/img/cPanel_AdvancedOptions.png)

  * Phần **Select Theme**, tại phần này các bạn có thể lựa chọn giao diện cho Wordpress của mình. Nếu các bạn không muốn chọn hoặc đã có giao diện sẵn thì có thể bỏ qua phần này

    ![](/img/cPanel_SelectTheme.png)

Sau khi đã cấu hình đây đủ các bạn ấn ô ""**Install**"" để cài đặt. Khi cài đặt xong thì sẽ hiện thông báo như hình dưới. Giờ các bạn có thể vào domain của các bạn để kiểm tra website wordpress có bị lỗi gì không.

  ![](/img/cPanel_Wordpress_Done.png)

## 3. Cài đặt thông qua Git™ Version Control

Cách cài đặt này phù hợp với những người phát triển web hoặc quản trị viên muốn tự động hóa việc triển khai, theo dõi thay đổi mã nguồn, và quản lý phiên bản dễ dàng trên server.

* **Bước 1. Đăng nhập vào cPanel**

  Để đăng nhập vào trang cPanel của các bạn, các bạn cần thông qua đường dẫn:

  **http://yourdomain/cpanel**

  Hoặc thông qua port 2083:

  **http://yourdomain:2083**

  Các bạn nhớ thay **yourdomain** bằng các domain của các bạn.

  ![](/img/cPanel_LoginPage.png)

* **Bước 2. Mở Git™ Version Control**

  Trong cPanel, tìm tới phần "**Files**" và chọn **Git™ Version Control**.

  ![](/img/cPanel_Git_Version-Control.png)

* **Bước 3. Tạo hoặc clone repository**

  Các bạn nhấn ô "Create" để tạo hoặc clone repository nếu bạn đã có repository ở trên Github, Gitlab,...

  ![](/img/cPanel_Create_Git.png)

  Sau khi các bạn đã vào trang tạo repository của Git Version Control sẽ có vài mục cần lưu ý

  * **Clone a Repository**:
    
    + Nếu bạn muốn tạo một repository mới, giữ tắt mục Enable this toggle.
    
    + Nếu bạn muốn clone từ một repository từ xa, bật mục Enable this toggle và nhập URL của repository từ xa vào ô Clone URL (URL này có thể bắt đầu với http://, https://, ssh://, hoặc git://).

  **Repository Path**:
    
    + Nhập đường dẫn nơi bạn muốn lưu trữ repository trên server. Đường dẫn này sẽ nằm trong thư mục /home/username/ của bạn, ví dụ: /home/username/public_html/my_project.
    
    + Lưu ý: Không sử dụng ký tự hoặc dấu đặc biệt như ./, ../, khoảng trắng, và các ký tự như: \ * | " ' < > & @ $ { } [ ] ( ) ; ? : = % #`.

  **Repository Name**:
    
    + Đặt tên cho repository để bạn dễ quản lý trong cPanel. Tên này không ảnh hưởng đến chức năng của repository mà chỉ giúp bạn dễ nhận biết.

    + Lưu ý: Không sử dụng các ký tự < và > trong tên repository.

  Nếu bạn muốn tạo thêm nhiều repository, có thể chọn tùy chọn **Create Another** để không phải trở lại trang trước.

  Tại đây mình sẽ clone repository của wordpress để tạo một trang website bằng wordpress.

  ![](/img/cPanel_Clone_Wordpress.png)

  Các bạn vào "**File Manager**" trên cPanel để kiểm tra xem đã clone được Wordpress chưa.

  ![](/img/cPanel_Git_CloneDone.png)

* **Bước 4. Chuyển sang thư mục public_html**

  Sau khi đã clone repository của wordpress xong, các bạn chuyển các file wordpress sang thư mục "**public_html**"

  ![](/img/cPanel_Move_Public.png)

  Khi đã bạn đã clone thành công các file wordpress thành công thì các bạn bắt đầu cấu hình wordpress bình thường.

  Trong thư mục WordPress mà bạn vừa clone, tìm tệp **wp-config-sample.php** và đổi tên **thành wp-config.php**.

  Mở tệp **wp-config.php** và điền các thông tin cơ sở dữ liệu:

      define( 'DB_NAME', 'your_database_name' );
      define( 'DB_USER', 'your_database_user' );
      define( 'DB_PASSWORD', 'your_password' );
      define( 'DB_HOST', 'localhost' );

  Khi đã cấu hình xong các bạn truy cập vào tên miền của các bạn để tiến hành cài đặt wordpress như bình thường.

    ![](/img/cPanel_Git_Success.png)

# END