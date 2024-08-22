# Cài đặt MySQL

# Mục lục
- [Cài đặt MySQL](#cài-đặt-mysql)
- [Mục lục](#mục-lục)
- [I. Cài đặt MySQL](#i-cài-đặt-mysql)
- [II. Cấu hình MySQL](#ii-cấu-hình-mysql)
- [END](#end)
# I. Cài đặt MySQL

* **Bước 1: Cập nhật hệ thống**

    Trước tiên, hãy đảm bảo hệ thống của bạn đã được cập nhật:

    ``# yum update -y``

* **Bước 2: Cài đặt MySQL**

    Sau khi cập nhật hệ thống, bạn có thể cài đặt HAProxy bằng lệnh:

    ``# yum install mysql-server -y``

    ![](/img/Mysql_install.png)
    
* **Bước 3: Kiểm tra phiên bản MySQL**

    Để xác nhận rằng MySQL đã được cài đặt thành công, bạn có thể kiểm tra phiên bản bằng cách chạy:

    ``# mysqld -V``

    ![](/img/Mysql_V.png)

    bạn dùng lệnh ``# systemctl start mysqld`` để khởi động MySQL

Đây là những thao tác cài đặt MySQL, những thao tác này sẽ không yêu cầu các bạn cài đặt mật khẩu hay thực hiện các bước cấu hình nào khác. Tuy nhiên điều này sẽ khiến cho MySQL của bạn không được an toàn trước những tin tặc 



# II. Cấu hình MySQL

Đối với các bản cài đặt mới của MySQL, bạn sẽ cần chạy tập lệnh bảo mật đi kèm của DBMS(Database Management System). Tập lệnh này sẽ giúp thay đổi một số tùy chọn mặc định kém an toàn hơn cho những thứ như thông tin đăng nhập, quyền cho phép từ xa, người dùng anonymous và database test.

Bạn chạy lệnh:  ``# mysql_secure_installation``

Đầu tiên hệ thống sẽ hỏi bạn có muốn thiết Lập VALIDATE PASSWORD COMPONENT. Mục đích của VALIDATE PASSWORD giúp đảm bảo rằng mật khẩu của người dùng đạt yêu cầu về độ mạnh và bảo mật. Nó kiểm tra mật khẩu để đảm bảo rằng nó không dễ đoán hoặc dễ bị tấn công.

Khi bạn được hỏi có muốn thiết lập VALIDATE PASSWORD không, bạn có thể chọn một trong các tùy chọn:

* **Yes**: Nếu bạn chọn thiết lập thành phần này, MySQL sẽ yêu cầu mật khẩu phải đáp ứng các tiêu chuẩn bảo mật nhất định. Điều này giúp cải thiện bảo mật của hệ thống MySQL bằng cách ngăn chặn việc sử dụng mật khẩu yếu hoặc dễ đoán.

* **No**: Nếu bạn chọn không thiết lập, MySQL sẽ không kiểm tra độ mạnh của mật khẩu và người dùng có thể sử dụng mật khẩu yếu hơn. Điều này có thể giảm bảo mật của hệ thống.

Tại đây mình chọn **YES**

![](/img/Mysql_VALIDATE%20PASSWORD.png)

Sau khi bạn chọn YES bạn sẽ được yêu cầu chọn mức độ chính sách xác thực mật khẩu.

* **LOW (0)**:

    * Yêu cầu: Mật khẩu có độ dài tối thiểu 8 ký tự.

    * Chế độ này yêu cầu mật khẩu phải có ít yêu cầu bảo mật nhất, phù hợp nếu bạn muốn ít hạn chế hơn và không quá nghiêm ngặt với mật khẩu.

* **MEDIUM (1)**:

    * **Yêu cầu**: Mật khẩu có độ dài tối thiểu 8 ký tự, bao gồm các ký tự số, chữ cái viết hoa và viết thường, và ký tự đặc biệt.

    * Chế độ này cung cấp một mức độ bảo mật cao hơn, yêu cầu mật khẩu phải có sự kết hợp của nhiều loại ký tự để đảm bảo độ mạnh và tính bảo mật tốt hơn.

* **STRONG (2)**:

    * **Yêu cầu**: Mật khẩu có độ dài tối thiểu 8 ký tự, bao gồm các ký tự số, chữ cái viết hoa và viết thường, ký tự đặc biệt và phải không xuất hiện trong một tập tin từ điển (dictionary file).

    * Chế độ này yêu cầu mật khẩu phải rất mạnh và bao gồm tất cả các yếu tố bảo mật, cùng với việc kiểm tra chống lại một tập tin từ điển để tránh việc sử dụng các mật khẩu dễ đoán.

![](/img/Mysql_3lvpass.png)

Tại đây mình sẽ chọn 2.

Sau khi nhập mật khẩu xong, hệ thống sẽ đánh giá độ mạnh của mật khẩu mà bạn đã nhập và hiển thị thông báo về độ mạnh. Sau khi đánh giá hệ thống sẽ yêu cầu xác nhận mật khẩu nếu bạn hài lòng

![](/img/Mysql_strenghpass.png)

Tiếp theo, hệ thống sẽ hiện thông báo nói rằng: 

**Khi cài đặt MySQL, mặc định sẽ có một người dùng ẩn danh (anonymous user) được tạo ra. Đây là một tài khoản người dùng không có mật khẩu và không cần phải đăng ký, giúp việc cài đặt và thử nghiệm dễ dàng hơn. Tuy nhiên, để bảo mật hệ thống và chuẩn bị cho môi trường sản xuất, bạn nên xóa người dùng ẩn danh này.**

* **Nhấn y hoặc Y**: Nếu bạn chọn xóa người dùng ẩn danh, MySQL sẽ xóa tài khoản này, giúp tăng cường bảo mật hệ thống. Đây là một bước quan trọng trước khi chuyển sang môi trường sản xuất hoặc khi bạn muốn đảm bảo rằng chỉ những người dùng có tài khoản và quyền hạn cụ thể mới có thể truy cập MySQL.

* **Nhấn phím khác**: Nếu bạn không muốn xóa người dùng ẩn danh, tài khoản này sẽ vẫn tồn tại. Điều này không phải là một vấn đề lớn trong môi trường thử nghiệm, nhưng không được khuyến khích trong môi trường sản xuất vì có thể tạo ra lỗ hổng bảo mật.

![](/img/Mysql_anyuser.png)

Để bảo mật hệ thống MySQL của bạn, hãy nhấn **y** và Enter để xóa người dùng ẩn danh. Đây là một phần của quy trình bảo mật cơ bản khi chuẩn bị hệ thống cho môi trường sản xuất.

Tiếp đến sẽ có thông báo nói rằng:

**Khi cài đặt MySQL, bạn sẽ được hỏi về việc cấm đăng nhập từ xa đối với tài khoản root. Đây là một bước quan trọng để bảo mật hệ thống của bạn.**

* **Nhấn y hoặc Y**: Chọn tùy chọn này để cấm tài khoản root đăng nhập từ xa. Điều này có nghĩa là tài khoản root chỉ có thể kết nối đến MySQL từ localhost (máy chủ hiện tại), không cho phép kết nối từ các địa chỉ IP khác. Đây là một biện pháp bảo mật quan trọng giúp giảm nguy cơ bị tấn công từ xa, vì chỉ những người có quyền truy cập trực tiếp vào máy chủ mới có thể sử dụng tài khoản root.

* **Nhấn phím khác**: Nếu bạn không chọn cấm đăng nhập từ xa, tài khoản root sẽ có thể đăng nhập từ các máy khác ngoài localhost, điều này có thể tạo ra rủi ro bảo mật nếu mật khẩu root bị lộ hoặc bị đoán từ xa.

Để tăng cường bảo mật hệ thống MySQL của bạn, hãy nhấn **y** và Enter để cấm đăng nhập từ xa đối với tài khoản root. Điều này giúp bảo vệ tài khoản quản trị chính của bạn khỏi các cuộc tấn công từ xa và chỉ cho phép truy cập trực tiếp từ máy chủ cài đặt MySQL.

![](/img/Mysql_allowroot.png)

Kế tiếp có thông báo:

**Khi cài đặt MySQL, hệ thống mặc định sẽ tạo ra một cơ sở dữ liệu tên là test, mà bất kỳ ai cũng có thể truy cập. Cơ sở dữ liệu này thường được sử dụng cho mục đích thử nghiệm và không nên được giữ lại trong môi trường sản xuất để đảm bảo bảo mật.**

* **Nhấn y hoặc Y**: Nếu bạn chọn xóa cơ sở dữ liệu test, MySQL sẽ loại bỏ cơ sở dữ liệu này cùng với quyền truy cập của nó. Điều này giúp giảm thiểu rủi ro bảo mật vì không còn cơ sở dữ liệu không cần thiết có thể bị truy cập bởi những người không được phép.

* **Nhấn phím khác**: Nếu bạn không chọn xóa cơ sở dữ liệu test, cơ sở dữ liệu này sẽ vẫn tồn tại và có thể bị truy cập bởi bất kỳ ai. Trong môi trường sản xuất, điều này có thể tạo ra lỗ hổng bảo mật không cần thiết.

Để đảm bảo môi trường MySQL của bạn an toàn và sạch sẽ trước khi chuyển sang môi trường sản xuất, hãy nhấn y và Enter để xóa cơ sở dữ liệu test và quyền truy cập của nó. Điều này giúp bạn loại bỏ các tài nguyên không cần thiết và giảm nguy cơ bị tấn công.

![](/img/Mysql_Databasetest.png)

Cuối cùng, hệ thống sẽ yêu cầu bạn có muốn làm mới các bảng quyền trong MySQL.

* **Nhấn y hoặc Y:** Nếu bạn chọn làm mới các bảng quyền, MySQL sẽ áp dụng ngay lập tức tất cả các thay đổi về quyền và cấu hình mà bạn đã thực hiện (như thay đổi mật khẩu, xóa người dùng ẩn danh, cấm đăng nhập từ xa cho root, xóa cơ sở dữ liệu test, v.v.). Điều này đảm bảo rằng các thay đổi này có hiệu lực ngay lập tức mà không cần khởi động lại dịch vụ MySQL.

* **Nhấn phím khác:** Nếu bạn không làm mới bảng quyền ngay lập tức, các thay đổi bạn đã thực hiện sẽ không có hiệu lực ngay cho đến khi bạn khởi động lại MySQL hoặc làm mới bảng quyền sau này.

Để đảm bảo rằng tất cả các thay đổi về cấu hình và quyền của bạn được áp dụng ngay lập tức, hãy nhấn **y** và Enter để làm mới các bảng quyền. Điều này giúp bạn tránh phải thực hiện lại các thay đổi hoặc khởi động lại MySQL để các thay đổi có hiệu lực.

![](/img/Mysql_privilege.png)

# END