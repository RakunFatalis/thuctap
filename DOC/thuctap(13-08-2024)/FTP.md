# FTP

# Mục lục

- [FTP](#ftp)
- [Mục lục](#mục-lục)
- [I. FTP là gì?](#i-ftp-là-gì)
- [II. Mô hình và nguyên lý hoạt động](#ii-mô-hình-và-nguyên-lý-hoạt-động)
  - [1. Mô hình FTP](#1-mô-hình-ftp)
    - [a. Phía Server](#a-phía-server)
    - [b. Phía Client](#b-phía-client)
  - [2. Nguyên lý hoạt động của FTP](#2-nguyên-lý-hoạt-động-của-ftp)
- [III. Tìm hiểu Normal Data Connections và Passive Data Connections](#iii-tìm-hiểu-normal-data-connections-và-passive-data-connections)
  - [1. Normal Data Connections](#1-normal-data-connections)
  - [2. Passive Data Connections](#2-passive-data-connections)
- [IV. Cài đặt FTP server sử dụng ProFTP](#iv-cài-đặt-ftp-server-sử-dụng-proftp)
  - [Cài đặt ProFTP trên Ubuntu](#cài-đặt-proftp-trên-ubuntu)
  - [Cấu hình cơ bản ProFTPD](#cấu-hình-cơ-bản-proftpd)
- [V. Thêm người dùng FPT và phân quyền](#v-thêm-người-dùng-fpt-và-phân-quyền)
- [VI. Một số lệnh làm việc với FTP qua CLI](#vi-một-số-lệnh-làm-việc-với-ftp-qua-cli)
- [VII. Bắt gói tin FTP tìm user và password của client khi dùng FTP plaintext và cách khắc phục](#vii-bắt-gói-tin-ftp-tìm-user-và-password-của-client-khi-dùng-ftp-plaintext-và-cách-khắc-phục)
- [END.](#end)



# I. FTP là gì?

FTP (File Transfer Protocol) là một giao thức máy tính với chức năng truyền tải tập tin và dữ liệu giữa các thiết bị với nhau thông qua TCP hoặc mạng Internet. Nhờ vào giao thức này, người sử dụng có thể dễ dàng truyền tải các tập tin như hình ảnh, văn bản, nhạc, video và các dữ liệu khác giữa máy tính cá nhân của họ và máy chủ đặt ở một nơi khác.

# II. Mô hình và nguyên lý hoạt động

## 1. Mô hình FTP

![](/img/FTP_stucture.png)

Do chức năng điều khiển và dữ liệu được truyền tải bằng cách sử dụng các kênh riêng biệt nên mô hình FTP chia mỗi thiết bị thành 2 phần giao thức logic chịu trách nhiệm cho mỗi kết nối ở trên:

* **Protocol interpreter (PI)**: Là thành phần quản lý kênh điều khiển, phát và nhận lệnh và trả lời.

* **Data transfer process (DTP)**: chịu trách nhiệm gửi và nhận dữ liệu giữa client và server.

### a. Phía Server

* **Server Protocol Interpreter (Server-PI)** : Chịu trách nhiệm quản lí Control Connection trên Server. Nó lắng nghe yêu cầu kết nối hướng từ User trên cổng 21. Khi kết nối được thiết lập, nó nhận lệnh từ User-PI, gửi phản hồi và quản lí tiến trình truyền dữ liệu trên Server.

* **Server Data Transfer Process (Server-DTP)** : Chịu trách nhiệm nhận và gửi file từ User-DTP. Server-DTP vừa làm nhiệm vụ thiết lập Data Connection và lắng nghe Data Connection của User thông qua cổng 20. Nó tương tác với Server File System trên hệ thống cục bộ để đọc và chép file.

### b. Phía Client

* **User Interface**: Đây là chương trình được chạy trên máy tính, nó cung cấp giao diện xử lí cho người dùng, chỉ có trên phía Client. Nó cho phép người dùng sử dụng những lệnh đơn giản để điều khiển các session FTP, từ đó có thể theo dõi được các thông tin và kết quả xảy ra trong quá trình.

* **User Protocol Interpreter (User-PI)**: Chịu trách nhiệm quản lí Control Connection phía Client. Nó khởi tạo phiên kết nối FTP bằng việc phát hiện ra Request tới Server-PI. Sau khi kết nối được thiết lập, nó xử lí các lệnh nhận được trên User Interface, gửi chúng tới Server-PI rồi đợi nhận Response trở lại. Nó cũng quản lí các tiến trình trên Client.

* **User Data Transfer Process (User-DTP)**: Có nhiệm vụ gửi hoặc nhận dữ liệu từ Server-DTP. User-DTP có thể thiết lập hoặc lắng nghe DataConnection từ Server thông qua cổng 20. Nó tương tác với Client File System trên Client để lưu trữ file.

## 2. Nguyên lý hoạt động của FTP

Cần có 2 kết nối TCP trong phiên làm việc của FTP: ``TCP Data connection`` trên cổng 20, ``TCP Control connection`` trên cổng 21.

* **Control connection** : luôn được mở ở mọi thời điểm khi dữ liệu hoặc lệnh được gửi.

* **Data connection** : chỉ được mở khi có trao đổi dữ liệu thực.

**Trình tự hoạt động chung của FTP**:

1. **FTP Client** mở Control connection đến FTP server (trên port 21) và chỉ định 1 cổng trên Client để Server gửi lại phản hồi. Đường kết nối này dùng để truyền lệnh và không phải là dữ liệu. Control connection sẽ mở trong suốt thời gian của phiên làm việc (telnet giữa 2 hệ thống).

2. **Client** chuyển tiếp thông tin như username, password tới Server để thực hiện xác thực (authentication). Server sẽ trả lời bằng mã chấp nhận hay từ chối của các request.

3. **Client** gửi thêm các lệnh với tên tệp, kiểu dữ liệu, … để vận chuyển, thêm luồng dữ liệu(tức là chuyển tập tin từ máy khách đến máy chủ hoặc ngược lại). Server sẽ phản hồi với mã (reply code) chấp nhận hoặc từ chối.

4. Khi dữ liệu đã sẵn sàng, 2 bên sẽ mở kết nối TCP trên cổng 20.

5. Dữ liệu có thể được vận chuyển giữa Client và Server trên cổng 20. Dữ liệu vận chuyển được mã hóa theo 1 số định dạng bao gồm ``NVT-ASCII`` hoặc ``nhị phân`` (binary).

6. Khi quá trình vận chuyển dữ liệu được hoàn thành, phiên làm việc của FTP Server sẽ đóng lại Data Connection trên cổng 20. Nhưng vẫn giữ Control Connection trên cổng 21.

7. Control connection có thể được sử dụng để thiết lập truyền dữ liệu khác hoặc đóng liên kết.

# III. Tìm hiểu Normal Data Connections và Passive Data Connections

Trong giao thức FTP (File Transfer Protocol), có hai chế độ kết nối chính mà máy khách (client) và máy chủ (server) có thể sử dụng để truyền dữ liệu: Normal Mode và Passive Mode.


## 1. Normal Data Connections

Trong chế độ Normal Data Connections(hay còn được gọi là Active Mode) FTP, quá trình kết nối giữa máy khách và máy chủ diễn ra theo các bước cụ thể:

1. **Máy khách khởi tạo kết nối**: Máy khách bắt đầu bằng việc kết nối từ một cổng ngẫu nhiên (N, nơi N > 1024) đến cổng 21 của máy chủ FTP. Đây là cổng lệnh (command port) tiêu chuẩn của FTP.

2. **Máy khách chuẩn bị cho kết nối dữ liệu**: Sau khi thiết lập kết nối điều khiển, máy khách bắt đầu lắng nghe trên cổng N+1 và gửi lệnh PORT N+1 đến máy chủ FTP. Lệnh này cho biết máy chủ rằng máy khách sẽ sử dụng cổng N+1 cho kết nối dữ liệu.

3. **Máy chủ khởi tạo kết nối dữ liệu**: Máy chủ FTP sử dụng cổng 20 của mình (cổng dữ liệu tiêu chuẩn của FTP) để kết nối đến cổng N+1 của máy khách, nơi máy khách đang lắng nghe.

Ảnh dưới minh hoạ các bước của Active Mode

![](/img/FTP_Activemode.png)

Các bước thể hiện trong ảnh:

* **Bước 1**: Máy khách sử dụng cổng lệnh của mình (cổng 1026) để liên lạc với cổng lệnh của máy chủ (cổng 21) và gửi lệnh PORT 1027. Lệnh này thông báo cho máy chủ biết rằng máy khách sẽ sử dụng cổng 1027 để thiết lập kết nối dữ liệu.

* **Bước 2**: Máy chủ gửi một thông báo ACK trở lại cổng lệnh của máy khách (cổng 1026) để xác nhận đã nhận được lệnh PORT.

* **Bước 3**: Máy chủ khởi tạo kết nối từ cổng dữ liệu của nó (cổng 20) đến cổng dữ liệu mà máy khách đã chỉ định trước đó (cổng 1027).

* **Bước 4**: Máy khách sau đó gửi một thông báo **ACK** trở lại cổng dữ liệu của máy chủ (cổng 20) để xác nhận rằng kết nối dữ liệu đã được thiết lập thành công.

Vấn đề chính với **Active mode FTP** thực tế nằm ở phía máy khách. Máy khách FTP không thực hiện kết nối thực sự đến cổng dữ liệu của máy chủ, nó chỉ đơn giản là thông báo cho máy chủ biết cổng mà nó đang lắng nghe, và sau đó máy chủ sẽ kết nối lại với cổng được chỉ định trên máy khách. Từ góc nhìn của tường lửa phía máy khách, điều này giống như một hệ thống bên ngoài đang khởi tạo kết nối đến một máy khách nội bộ điều mà thường sẽ bị chặn.

## 2. Passive Data Connections

Để giải quyết vấn đề khi máy chủ khởi tạo kết nối đến máy khách, một phương pháp khác cho các kết nối FTP đã được phát triển. Phương pháp này được gọi là Passive Data Connections(hay còn được gọi là Passive Mode). Sau khi câu lệnh được sử dụng bởi máy khách để thông báo cho máy chủ rằng nó đang ở chế độ passive mode.

Trong chế độ passive mode, máy khách khởi tạo cả hai kết nối đến máy chủ, giải quyết vấn đề của việc tường lửa lọc các kết nối cổng dữ liệu đến máy khách từ máy chủ. Khi mở một kết nối FTP, máy khách mở hai cổng ngẫu nhiên không được cấp quyền (N > 1024 và N+1) ở phía địa phương. Cổng đầu tiên liên hệ với máy chủ trên cổng 21, nhưng thay vì phát lệnh **PORT** và cho phép máy chủ kết nối ngược lại đến cổng dữ liệu của nó, máy khách sẽ phát lệnh **PASV**. Kết quả là máy chủ mở một cổng ngẫu nhiên không được cấp quyền (P > 1024) và gửi lệnh PORT P lại cho máy khách. Sau đó, máy khách sẽ khởi tạo kết nối từ cổng N+1 đến cổng P trên máy chủ để truyền dữ liệu.

Từ quan điểm của tường lửa phía máy chủ, để hỗ trợ chế độ thụ động FTP, các cổng sau cần được mở:

* Cổng 21 của máy chủ FTP từ bất kỳ đâu (Máy khách khởi tạo kết nối)

* Cổng 21 của máy chủ FTP đến các cổng > 1024 (Máy chủ phản hồi đến cổng điều khiển của máy khách)

* Các cổng > 1024 của máy chủ FTP từ bất kỳ đâu (Máy khách khởi tạo kết nối dữ liệu đến cổng ngẫu nhiên do máy chủ chỉ định)

* Các cổng > 1024 của máy chủ FTP đến các cổng > 1024 từ xa (Máy chủ gửi ACK (và dữ liệu) đến cổng dữ liệu của máy khách)

Ảnh dưới minh hoạ các bước trong chế độ Passive Mode:

![](/img/FTP_Passivemode.png)

Giải thích các bước trong hình:

* **Bước 1**: Máy khách gửi lệnh PASV đến máy chủ qua cổng điều khiển (cổng 21) để yêu cầu chế độ thụ động.

* **Bước 2**: Máy chủ phản hồi bằng lệnh PORT 2024, thông báo cho máy khách cổng số 2024 mà máy chủ sẽ sử dụng để nhận kết nối dữ liệu.

* **Bước 3**: Máy khách mở một kết nối từ cổng dữ liệu của nó đến cổng dữ liệu 2024 của máy chủ để truyền dữ liệu.

* **Bước 4**: Máy chủ gửi lại một xác nhận (ACK) đến cổng dữ liệu của máy khách để xác nhận rằng kết nối dữ liệu đã được thiết lập thành công.

Mặc dù chế độ passive mode giải quyết nhiều vấn đề từ phía máy khách, nó mở ra một loạt các vấn đề về bảo mật phía máy chủ. Vấn đề lớn nhất là cần phải cho phép bất kỳ kết nối từ xa nào đến các cổng số cao trên máy chủ. May mắn thay, FTP daemons cho phép quản trị viên chỉ định một dải cổng mà máy chủ FTP sẽ sử dụng.

# IV. Cài đặt FTP server sử dụng ProFTP

``Pro-FTP`` là một ứng dụng tạo ra dịch vụ truyền file với giao thức FTP (File Transfer Protocol), từ đó có thể truy cập các file của Server. Các máy khách client có thể truy cập đến bằng các trình FPT Client ví dụ như: WinSCP, Cyberduck, FileZilla …

Mình có một máy ảo Ubuntu có địa chỉ IP: ``192.168.3.174`` để làm bài lab này.
## Cài đặt ProFTP trên Ubuntu

Sử dụng câu lệnh sau để cập nhật danh sách gói:

``# apt update``

Chạy lệnh sau để cài đặt ProFTPD:

``# apt install proftpd -y``

![](/img/FTP_installproftp.png)

Sau khi cài đặt, dịch vụ ProFTPD sẽ tự động khởi động. Nếu không, bạn có thể khởi động bằng lệnh:

``# systemctl start proftpd``

Kiểm tra trạng thái của ProFTPD bằng câu lệnh:

``# systemctl status proftpd``

![](/img/FTP_status.png)

## Cấu hình cơ bản ProFTPD

Bạn sẽ tìm thấy file cấu hình của ProFTPD trong thư mục /``etc/proftpd``. Mở file bằng nano bằng cách chạy:

``# nano /etc/proftpd/proftpd.conf``

![](/img/FTP_fileconfig.png)

Trong dòng ``Servername``, hãy thay thế giá trị bằng tên máy chủ hoặc miền của bạn:

        ServerName "192.168.3.174"

![](/img/FPT_ServerName.png)

Bỏ ghi chú dòng ``DefaultRoot`` để kích hoạt tính năng jail cho tất cả người dùng:

![](/img/FPT_Deroot.png)

Và khởi động lại ProFTPD thông qua lệnh systemctl theo cách sau.

``# systemctl restart proftpd``

Mở cổng 21 cho FTP:

``# ufw allow 21/tcp``

``# ufw reload``

Kết nối máy chủ FPT:

``# fpt 192.168.3.174``

![](/img/FPT_login.png)

# V. Thêm người dùng FPT và phân quyền

Có hai loại người dùng FTP có sẵn, người dùng FTP ẩn danh và người dùng FTP 'bình thường':

* **FTP ẩn danh**: Máy chủ FTP cung cấp quyền truy cập cho bất kỳ ai mà không cần phải có tài khoản người dùng và mật khẩu. Điều này không nên được sử dụng trên một máy chủ có sẵn công khai, nhưng có thể là một tùy chọn cho máy chủ gia đình hoặc mạng LAN công ty.

* **Người dùng FTP**: Chỉ những người có tài khoản người dùng và mật khẩu mới có thể truy cập vào máy chủ FTP.

* **Cấu hình cho FTP ẩn danh:**

    Mở file cấu hình ProFTPD bằng lệnh:

    ``# nano /etc/proftpd/proftpd.conf``

    Để cấu hình phân quyền cho FTP ẩn danh, bạn cần chỉ định thư mục mà người dùng ẩn danh có thể đọc được nhưng không thể ghi (tải lên) file. Ví dụ, nếu bạn muốn phân quyền cho người dùng ẩn danh chỉ đọc từ thư mục /srv/ftp, bạn có thể thêm cấu hình sau:

    ![](/img/FPT_userano.png)

    ``UserAlias anonymous ftp``: Cho phép người dùng đăng nhập bằng tên anonymous hoặc ftp.
    
    ``<Directory /srv/ftp>``: Xác định thư mục /srv/ftp cho người dùng ẩn danh.
    
    ``<Limit WRITE> DenyAll``: Ngăn không cho người dùng ẩn danh tải lên hoặc ghi file.
    
    ``<Limit READ> AllowAll``: Cho phép người dùng ẩn danh đọc file.

    Ta khởi động lại FTP để áp dụng cấu hình:

    ``# systemctl restart proftpd``

    Ta đăng nhập FPT bằng tài khoản ẩn danh. Tài khoản ẩn danh sẽ không yêu cầu mật khẩu mà chỉ cần địa chỉ email của mình hoặc ta có thể để trống.

    ![](/img/FPT_anologin.png)

* **Cấu hình người dùng FPT:**

    Trước tiên, bạn cần tạo tài khoản người dùng trên hệ thống. Tài khoản này sẽ được sử dụng để đăng nhập vào máy chủ FTP.

    ``# adduser ftpuser``

    Thiết lập quyền thư mục cho người dùng:

    ``# mkdir -p /home/ftpuser/uploads``
    
    ``# chown ftpuser:ftpuser /home/ftpuser/uploads``

    ``# chmod 755 /home/ftpuser``

    ``# chmod 755 /home/ftpuser/uploads``

    Như cách ta làm như phần người dùng ẩn danh, ta vào thư mục ``proftpd.conf`` nội dụng của file cấu hình như sau:

    ![](/img/FTP_userconf.png)

    Ta kết nối FTP:

    ![](/img/FTP_userlogin.png)



# VI. Một số lệnh làm việc với FTP qua CLI

| Lệnh                | Mô tả                                              | Ví dụ                    |
|---------------------|---------------------------------------------------|--------------------------|
| `ftp <IP>`          | Kết nối đến máy chủ FTP                           | `ftp 192.168.3.139`     |
| `ls`                | Liệt kê các file và thư mục trong thư mục hiện tại | `ls`                    |
| `cd <thư-mục>`      | Thay đổi thư mục làm việc                         | `cd uploads`            |
| `pwd`               | Hiển thị thư mục làm việc hiện tại                | `pwd`                   |
| `get <file>`        | Tải xuống một file từ máy chủ FTP                  | `get example.txt`       |
| `put <file>`        | Tải lên một file từ máy tính đến máy chủ FTP       | `put localfile.txt`     |
| `mget <pattern>`    | Tải xuống nhiều file theo mẫu                     | `mget *.txt`            |
| `mput <pattern>`    | Tải lên nhiều file theo mẫu                       | `mput *.txt`            |
| `delete <file>`     | Xóa một file trên máy chủ FTP                     | `delete oldfile.txt`    |
| `mkdir <dir>`       | Tạo một thư mục mới trên máy chủ FTP              | `mkdir newdir`          |
| `rmdir <dir>`       | Xóa một thư mục trống trên máy chủ FTP            | `rmdir olddir`          |
| `bye`               | Ngắt kết nối và thoát khỏi phiên FTP              | `bye`                   |

# VII. Bắt gói tin FTP tìm user và password của client khi dùng FTP plaintext và cách khắc phục

FTP là một phương pháp truyền tập tin có truyền thống phi bảo an (không an toàn), vì theo như bản thiết kế gốc đặc tả của FTP, không có cách nào có thể truyền tải dữ liệu dưới hình thức mật mã hóa được. Ảnh hưởng này có nghĩa là, phần lớn các cài đặt của mạng lưới truyền thông, tên người dùng, mật khẩu, dòng lệnh FTP và tập tin được truyền tải, đều có thể bị người khác trên cùng một mạng lưới, “ngửi” hoặc quan sát, dùng phần mềm phân tích giao thức (protocol analyzer) (hoặc còn gọi là “dụng cụ ngửi dữ liệu”, tiếng Anh là “sniffer”).

**Ví dụ:** Mình đang có một máy chủ FTP với địa chỉ IP là: ``192.168.0.176`` đang kết nối với mạng công cộng. Và giả sử mình có một máy khách đăng nhập vào máy chủ FTP này để up file lên và có một tin tặc biết rằng mình sẽ đăng nhập vào máy chủ FTP. Hắn sẽ thử bắt gói tin của cổng 21 (cổng mặc định của FTP) nếu máy chủ không cấu hình mã hoá thì tất cả thông tin mình nhập sẽ hiện lên trên con máy tính của tên tin tặc đó.

Dưới đây là hình ảnh hiển thị của tin tặc khi bắt được gói thông tin.

![](/img/FTP_goitin.png)

Tại đây hắn đã biết được thông tài khoản và mật khẩu của máy khách, điều này cực kì nguy hiểm đối với việc bảo mật.

**Cách khắc phục:**

 1. **Sử dụng SFTP**
    
    **SFTP (Secure File Transfer Protocol)** là một giao thức mạng dùng để truyền tải và quản lý tệp tin một cách bảo mật qua một kết nối mạng. SFTP hoạt động dựa trên SSH (Secure Shell), do đó nó cung cấp một lớp bảo mật mạnh mẽ bằng cách mã hóa dữ liệu trong quá trình truyền tải, giúp bảo vệ thông tin khỏi các nguy cơ bị nghe lén hoặc bị sửa đổi.
  
2. **Sử dụng FTPS:**

    **FTPS (FTP Secure hoặc FTP-SSL)** là một phiên bản bảo mật của FTP (File Transfer Protocol). FTPS cải thiện bảo mật của FTP bằng cách thêm các lớp mã hóa SSL (Secure Sockets Layer) hoặc TLS (Transport Layer Security) để bảo vệ dữ liệu trong quá trình truyền tải.

3. **Sử dụng VPN:**

    **VPN (Virtual Private Network)** là một công nghệ mạng cho phép tạo ra một kết nối mạng an toàn và mã hóa qua Internet. VPN giúp bảo vệ dữ liệu và thông tin cá nhân khi bạn truy cập vào mạng công cộng, chẳng hạn như Wi-Fi công cộng, bằng cách tạo ra một "đường hầm" mã hóa giữa thiết bị của bạn và máy chủ VPN.

4. **Xác thực 2 bước:**

    **Xác thực 2 bước (2FA)** là phương pháp bảo mật quản lý truy nhập và danh tính yêu cầu hai hình thức nhận dạng để truy nhập tài nguyên và dữ liệu. 2FA cung cấp cho các doanh nghiệp khả năng giám sát, đồng thời giúp bảo vệ những thông tin và mạng dễ bị tấn công nhất của họ.

5. **Cấu hình tường lửa**

    Cấu hình tường lửa để hạn chế quyền truy cập vào máy chủ FTP từ các địa chỉ IP không đáng tin cậy hoặc từ các mạng không an toàn. Đồng thời phải theo dõi các bản ghi (log) của tường lửa để phát hiện các hoạt động đáng ngờ hoặc trái phép.

# END.