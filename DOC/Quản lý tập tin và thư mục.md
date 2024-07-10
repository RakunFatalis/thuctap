# QUẢN LÝ TẬP TIN VÀ THƯ MỤC

# MỤC LỤC

## I. Cấu trúc thư mục của Linux

Linux quản lý hệ thống trên một "hệ thống tệp tin" duy nhất, bắt đầu ở gốc là thư mục root (`/`), đây là thư mục ở cấp cao nhất. Cấu trúc cơ bản của hệ thống Linux như sau:

![Filesystem Structure](/thuctap/img/filesystemlinux.png)

Trong đó:

| Thư mục | Miêu tả |
| ------- | ------- |
| `/` | Nó là thư mục chính mà chỉ chứa các thư mục cần thiết ở cấp cao nhất trong cấu trúc file. |
| `/bin` | Vị trí này đặt các file có thể chạy được. Chúng có sẵn cho mọi người dùng. |
| `/boot` | Chứa các file để khởi động hệ thống (boot). |
| `/dev` | Thư mục đặc biệt chứa các tập tin đại diện cho các thiết bị phần cứng và các thiết bị ảo (virtual devices) |
| `/etc` | Các lệnh thư mục Supervisors, các file định cấu hình, các file định cấu hình đĩa, danh sách người dùng hợp lệ, ethernet, host, là nơi để gửi các thông điệp nghiêm trọng. |
| `/home` | Chứa thư mục chính cho các người sử dụng và các tài khoản khác. |
| `/lib` | Chứa các file thư viện được chia sẻ và đôi khi các tệp liên quan đến Kernel. |
| `/media` | Thư mục này được sử dụng để tự động gắn kết các phương tiện di động như ổ USB, đĩa CD-ROM và đĩa DVD. Các bản phân phối Linux hiện đại thường sử dụng thư mục này để tự động gắn kết các thiết bị này khi chúng được chèn vào. |
| `/mnt` | Sử dụng để gắn kết (mount) các hệ thống file tạm thời, như cdroom và đĩa mềm. |
| `/opt` | Thư mục này được sử dụng để cài đặt các gói phần mềm tùy chọn. Nó thường được sử dụng cho các ứng dụng của bên thứ ba không phải là một phần của cài đặt hệ thống tiêu chuẩn. |
| `/proc` | Chứa tất cả các tiến trình được đánh dấu như một file bởi số tiến trình hoặc thông tin khác mà là động lực của hệ thống. |
| `/root` | Thư mục này là thư mục chính của người dùng root, người có quyền siêu người dùng với các đặc quyền quản trị. |
| `/sbin` | Thư mục này chứa các tệp nhị phân hệ thống cần thiết được sử dụng cho các tác vụ quản trị hệ thống. Các chương trình này thường được sử dụng bởi người dùng root hoặc các người dùng khác có quyền phù hợp. |
| `/srv`|   Thư mục được sử dụng để chứa dữ liệu của các dịch vụ (services) của hệ thống. Các dịch vụ này có thể là các ứng dụng web, FTP, hay các dịch vụ mạng khác.|
| `/tmp`|Thư mục đặc biệt được sử dụng để lưu trữ tạm thời các tệp tin và thư mục. Đây là nơi mà các ứng dụng có thể lưu trữ dữ liệu tạm thời trong quá trình hoạt động.|
|`/usr`|Thư mực chứa các tệp và thư mục chính của hệ thống, bao gồm các chương trình, thư viện, tài liệu và các tài nguyên hệ thống chung.|
|`/var`|Thư mục lưu trữ dữ liệu biến đổi trong quá trình hoạt động của hệ thống, bao gồm các tệp log, cơ sở dữ liệu tạm thời, mail, và các tệp tin khác có thể thay đổi kích thước.|

## II.  Các lệnh quản lý tập tin và thư mục
### 1. Tạo, xóa, di chuyển, và sao chép tập tin/thư mục


