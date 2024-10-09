# mySQL

# Mục lục

- [mySQL](#mysql)
- [Mục lục](#mục-lục)
- [I. MySQL là gì ?](#i-mysql-là-gì-)
- [II. Lịch sử hình thành và phát triển của MySQL ?](#ii-lịch-sử-hình-thành-và-phát-triển-của-mysql-)
  - [1. Sự Hình Thành (1994 - 1996)](#1-sự-hình-thành-1994---1996)
  - [2. Phát Triển và Mở Rộng (1996 - 2000)](#2-phát-triển-và-mở-rộng-1996---2000)
  - [3. Phát Triển Vượt Bậc và Sáp Nhập (2000 - 2008)](#3-phát-triển-vượt-bậc-và-sáp-nhập-2000---2008)
  - [4. Giai Đoạn Oracle và Phát Triển Tiếp Tục (2010 - Nay)](#4-giai-đoạn-oracle-và-phát-triển-tiếp-tục-2010---nay)
- [III. Các thuật ngữ liên quan đến mySQL](#iii-các-thuật-ngữ-liên-quan-đến-mysql)
- [IV. MySQL hoạt động như thế nào?](#iv-mysql-hoạt-động-như-thế-nào)
- [V. Các đặc tính của MySQL](#v-các-đặc-tính-của-mysql)
- [END](#end)

# I. MySQL là gì ?

MySQL là một hệ thống quản trị cơ sở dữ liệu mã nguồn mở (**Relational Database Management System**, viết tắt là RDBMS) hoạt động ở mô hình **client-server**. RDBMS là một phần mềm hay dịch vụ dùng để tạo và quản lý các cơ sở dữ liệu (Database) o hình thức quản lý các mối liên hệ giữa chúng.

MySQL là một trong số các phần mềm RDBMS. RDBMS và MySQL thường được cho là một vì độ phổ biến quá lớn của MySQL. Các ứng dụng web lớn nhất như Facebook, Twitter, YouTube, Google, và Yahoo! đều dùng MySQL cho mục đích lưu trữ dữ liệu. Kể cả khi ban đầu nó chỉ được dùng rất hạn chế nhưng giờ nó đã tương thích với nhiều hạ tầng máy tính quan trọng như Linux, macOS, Microsoft Windows, và Ubuntu.

![](/img/Mysql_logo.png)

# II. Lịch sử hình thành và phát triển của MySQL ?

## 1. Sự Hình Thành (1994 - 1996)
    
* **1994**: MySQL được phát triển lần đầu tiên bởi hai lập trình viên người Thụy Điển, Michael "Monty" Widenius và David Axmark, cùng với Allan Larsson. Dự án ban đầu bắt nguồn từ một dự án khác của họ là mSQL (mini SQL), nhưng họ quyết định viết lại toàn bộ để tạo ra một hệ thống cơ sở dữ liệu nhanh hơn và linh hoạt hơn.

* **1995**: Phiên bản đầu tiên của MySQL được phát hành vào ngày 23 tháng 5 năm 1995. Đây là một hệ quản trị cơ sở dữ liệu quan hệ (RDBMS) mã nguồn mở, sử dụng ngôn ngữ truy vấn SQL.

## 2. Phát Triển và Mở Rộng (1996 - 2000)

* **1996**: MySQL nhanh chóng trở nên phổ biến trong cộng đồng phát triển phần mềm mã nguồn mở nhờ tính đơn giản, hiệu suất cao và miễn phí. Trong giai đoạn này, MySQL đã được cải thiện đáng kể về tính năng và hiệu suất, đặc biệt là với việc bổ sung hỗ trợ cho các bảng chỉ mục và giao dịch.

* **1999**: Công ty MySQL AB được thành lập để quản lý và phát triển MySQL. Công ty này chịu trách nhiệm thương mại hóa MySQL thông qua việc cung cấp các dịch vụ hỗ trợ và phiên bản thương mại của phần mềm.

## 3. Phát Triển Vượt Bậc và Sáp Nhập (2000 - 2008)

* **2000**: MySQL 3.23 ra mắt với nhiều cải tiến lớn, bao gồm hỗ trợ giao dịch thông qua công cụ lưu trữ InnoDB, giúp MySQL trở thành một lựa chọn tốt cho các ứng dụng doanh nghiệp.

* **2003**: MySQL 4.0 được phát hành, mang lại khả năng xử lý các câu truy vấn phức tạp hơn và cải thiện hiệu suất.

* **2005**: MySQL 5.0 ra mắt, giới thiệu các tính năng quan trọng như stored procedures (thủ tục lưu trữ), triggers (kích hoạt), views (các quan điểm), và khóa ngoại, nâng cao đáng kể khả năng của MySQL trong các ứng dụng phức tạp.

* **2008**: **Sun Microsystems**, một công ty công nghệ lớn, mua lại MySQL AB với giá khoảng 1 tỷ USD. Thương vụ này giúp MySQL có thêm tài nguyên và sự hỗ trợ để phát triển tiếp.

## 4. Giai Đoạn Oracle và Phát Triển Tiếp Tục (2010 - Nay)

* **2010**: **Oracle Corporation** mua lại **Sun Microsystems**, do đó sở hữu luôn MySQL. Điều này gây lo ngại trong cộng đồng mã nguồn mở về việc MySQL có thể bị ảnh hưởng bởi sự kiểm soát của một công ty lớn. Tuy nhiên, Oracle cam kết tiếp tục phát triển MySQL như một dự án mã nguồn mở.

* **2013**: MySQL 5.6 được phát hành, mang đến nhiều cải tiến về hiệu suất, khả năng mở rộng, và bảo mật, cùng với nhiều tính năng mới.

* **2015**: MySQL 5.7 ra đời, với các cải tiến đáng kể trong khả năng thực hiện các truy vấn phức tạp, đồng thời cải thiện tối ưu hóa và hỗ trợ JSON.

* **2018**: MySQL 8.0 được phát hành, với nhiều cải tiến mạnh mẽ, như hỗ trợ bảng tổng hợp (CTE), các chỉ mục vô hình, bảng phân vùng, và tăng cường hiệu suất cho các ứng dụng hiện đại.

MySQL đã trở thành một công cụ quan trọng trong thế giới công nghệ, từ những ngày đầu chỉ là một dự án nhỏ cho đến khi trở thành một trong những hệ quản trị cơ sở dữ liệu được sử dụng rộng rãi nhất trên thế giới, hỗ trợ hàng triệu ứng dụng và website.

# III. Các thuật ngữ liên quan đến mySQL

* **Database**

    Database (cơ sở dữ liệu) là một tập hợp có cấu trúc của dữ liệu, được tổ chức và lưu trữ sao cho có thể dễ dàng truy cập, quản lý, và cập nhật. Dữ liệu trong database có thể được sắp xếp dưới dạng bảng (table), với các hàng (row) và cột (column), mỗi bảng thường đại diện cho một thực thể cụ thể như người dùng, sản phẩm, đơn hàng, v.v.

* **Open Source**

    Open Source là một khái niệm liên quan đến phần mềm mà mã nguồn (source code) của nó được công khai và có thể truy cập, sử dụng, sửa đổi và phân phối bởi bất kỳ ai. Điều này khác với phần mềm độc quyền, nơi mã nguồn được giữ bí mật và chỉ những người phát triển hoặc một nhóm nhỏ mới có quyền truy cập.

* **Mô hình Client-Server**

    Mô hình **Client-Server** là một kiến trúc mạng trong đó có hai thành phần chính: client (máy khách) và server (máy chủ). Mô hình này được sử dụng rộng rãi trong nhiều ứng dụng và dịch vụ trên internet, như web, email, và cơ sở dữ liệu.

# IV. MySQL hoạt động như thế nào?

MySQL hoạt động bằng cách cho phép người dùng tạo databases và tables, lưu trữ data trong chúng, và truy xuất thông tin từ các databases này khi cần. Chức năng của MySQL dựa trên mô hình client-server. Một máy chủ (server) là một máy tính lưu trữ phần mềm MySQL và các databases. Trong khi đó, máy khách (client) là phần mềm gửi yêu cầu tới máy chủ MySQL để thực hiện các thao tác trên databases.

MySQL sử dụng SQL (**Structured Query Language**) để thực hiện các tasks. Câu lệnh SQL là những hướng dẫn được đưa ra cho máy chủ MySQL để đọc, thao tác, hoặc kiểm soát data được lưu trữ trong các databases của nó. Ví dụ, command ``SELECT`` được sử dụng để truy xuất data từ database. Để thêm data mới, command ``INSERT`` được sử dụng. Tương tự, các commands ``DELETE`` và ``UPDATE`` được sử dụng để xoá hoặc cập nhật data hiện có.

Trong mô hình client-server, client thiết lập một kết nối với server thông qua mạng. Kết nối này cho phép người dùng truy cập các databases trên server và thực hiện các thao tác trên chúng bằng các câu lệnh SQL. Một khi một yêu cầu được gửi từ client, nó sẽ được server xử lý và kết quả sẽ được gửi lại cho client.

# V. Các đặc tính của MySQL

| **Đặc Tính**| **Mô Tả**|
|-------------|----------|
| **Mã nguồn mở (Open Source)**| MySQL là phần mềm mã nguồn mở, cho phép người dùng tải về, sử dụng và tùy chỉnh miễn phí, với các phiên bản thương mại có hỗ trợ kỹ thuật từ Oracle.  |
| **Hiệu suất cao (High Performance)**| MySQL được thiết kế để cung cấp hiệu suất cao, đặc biệt là trong môi trường web, xử lý tốt các tác vụ đọc và ghi dữ liệu lớn.|
| **Khả năng mở rộng (Scalability)**| MySQL có thể dễ dàng mở rộng để xử lý một lượng dữ liệu lớn mà vẫn duy trì hiệu suất cao.|
| **Tính di động (Portability)**| MySQL chạy trên nhiều hệ điều hành khác nhau như Windows, Linux, macOS, làm cho nó linh hoạt trong nhiều môi trường phát triển.|
| **Bảo mật cao (High Security)**| MySQL cung cấp các cơ chế bảo mật mạnh mẽ như mã hóa dữ liệu, quản lý tài khoản người dùng, và kiểm soát truy cập.|
| **Hỗ trợ đa người dùng (Multi-User)**| MySQL hỗ trợ đồng thời nhiều người dùng, cho phép thao tác trên cơ sở dữ liệu cùng lúc mà không ảnh hưởng đến hiệu suất.|
| **Hỗ trợ giao dịch (Transaction)**| MySQL hỗ trợ các giao dịch với các tính năng ACID (Atomicity, Consistency, Isolation, Durability), đảm bảo tính toàn vẹn của dữ liệu.|
| **Hỗ trợ nhiều loại dữ liệu (Data Types)** | MySQL hỗ trợ nhiều kiểu dữ liệu như số nguyên, chuỗi, ngày tháng, thời gian, và các loại dữ liệu đặc biệt như JSON và XML.|
| **Sao lưu và phục hồi (Backup/Recovery)** | MySQL cung cấp các công cụ sao lưu và phục hồi dữ liệu, giúp bảo vệ dữ liệu khỏi mất mát trong trường hợp sự cố.|
| **Tính tương thích (Compatibility)**| MySQL có thể tích hợp với nhiều ngôn ngữ lập trình và ứng dụng khác nhau, làm cho nó trở thành lựa chọn phổ biến cho các ứng dụng web và doanh nghiệp. |
| **Cộng đồng lớn (Community Support)**| MySQL có một cộng đồng người dùng lớn và nhiều tài liệu, diễn đàn hỗ trợ, cùng với các bản cập nhật thường xuyên từ Oracle.|

# END