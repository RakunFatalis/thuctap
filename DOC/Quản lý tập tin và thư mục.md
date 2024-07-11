# QUẢN LÝ TẬP TIN VÀ THƯ MỤC

# MỤC LỤC

- [QUẢN LÝ TẬP TIN VÀ THƯ MỤC](#quản-lý-tập-tin-và-thư-mục)
- [MỤC LỤC](#mục-lục)
  - [I. Cấu trúc thư mục của Linux](#i-cấu-trúc-thư-mục-của-linux)
  - [II.  Các lệnh quản lý tập tin và thư mục](#ii--các-lệnh-quản-lý-tập-tin-và-thư-mục)
    - [1. Các câu lệnh thao tác với file và thư mục (tạo, xóa, tìm kiếm, phân quyền…)](#1-các-câu-lệnh-thao-tác-với-file-và-thư-mục-tạo-xóa-tìm-kiếm-phân-quyền)
    - [2. Thay đổi quyền truy cập và chủ sở hữu](#2-thay-đổi-quyền-truy-cập-và-chủ-sở-hữu)
  - [III.  Nén và giải nén tập tin](#iii--nén-và-giải-nén-tập-tin)
    - [Các loại nén và giải nén](#các-loại-nén-và-giải-nén)
- [END](#end)
## I. Cấu trúc thư mục của Linux

Linux quản lý hệ thống trên một "hệ thống tệp tin" duy nhất, bắt đầu ở gốc là thư mục root (`/`), đây là thư mục ở cấp cao nhất. Cấu trúc cơ bản của hệ thống Linux như sau:

![Filesystem Structure](/img/filesystemlinux.png)

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

### 1. Các câu lệnh thao tác với file và thư mục (tạo, xóa, tìm kiếm, phân quyền…)

|Câu lệnh|Mục đích|
|--------|---------|
|`mkdir`|Tạo một thư mục|
|`touch`|Tạo một file mới|
|`rmdir`|Xóa một thư mục (chỉ xóa được file rỗng), muốn xóa thư mục không rỗng, các bạn dùng lệnh sau: `rm -rf`|
|`mv`   |Di chuyển hoặc đổi tên file|
|`rm`   |Xoá file|
|`cp`   |Copy một hay nhiều file đến folder mới|
|`chmod`|Phân quyền file, folder|
|`chown`|Đổi owner cho folder hay file.|
|`wget` |Sử dụng để tải xuống các tệp từ Internet|
|`find` |Sử dụng để tìm kiếm các tệp và thư mục trong cấu trúc thư mục hệ thống tệp    |

### 2. Thay đổi quyền truy cập và chủ sở hữu

* **Quyền truy cập căn bản:**
    1. **Read(R):** Cho phép đọc nội dung của tệp hoặc thự mục
    2. **Write(W):** Cho phép sửa đội nội dung của tệp hoặc thư mục
    3. **Excute(X):** Cho phép thực thi tệp hoặc thư mục

* **Quyền áp dụng cho người dùng:**:
    1. **Chủ sở hữu (Owner):** Người tạo ra tệp hoặc thư mục, có thể quyết định quyền truy cập của tệp hoặc thư mục.
    2. **Nhóm (Group):** Các người dùng thuộc nhóm có thể có các quyền riêng biệt.
    3. **Khác (Other):** Tất cả người dùng khác ngoài chủ sở hữu và nhóm.

* **Đọc hiểu được các kí tự phân quyền**
    
    Trong Linux, mọi thứ đều được coi như một file và khi sử dụng lệnh ``ls -l``, mỗi dòng sẽ hiển thị thông tin về một file hoặc thư mục.

    ![](/img/ls_L.png)

    Ta có thể thấy quyền được cấp của các thư mục và file được kí hiệu bởi 10 ký tự `-`

    Trong đó:
    
    **Ký tự đầu tiên:** Xác định loại tệp
    * `-`: Tệp thông thường
    * `d`: Thư mục
    * `l`: symbolic link
    * `c`: Thiết bị ký tự
    * `b`: block device
    * `p`: Pipe 
    * `s`: Socket 

    **Ký tự thứ 2 đến thứ 4:** Quyền của chủ sở hữu (Owner)

    * ``r``: Quyền đọc (read)
    * ``w``: Quyền ghi (write)
    * ``x``: Quyền thực thi (execute)
    * ``-``: Không có quyền
    
    **Ký tự thứ 5 đến thứ 7:** Quyền của nhóm (group)

    * ``r``: Quyền đọc
    * ``w``: Quyền ghi
    * ``x``: Quyền thực thi
    * ``-``: Không có quyền
    
    **Ký tự thứ 8 đến thứ 10:** Quyền của người khác (others)

    * ``r``: Quyền đọc
    * ``w``: Quyền ghi
    * ``x``: Quyền thực thi
    * ``-``: Không có quyền

    **Hình ảnh minh hoạ**

    ![](/img/file_permissions.png)

* **Cách sử dụng lệnh chmod để phân quyền**
    
    Có 2 cách phương pháp sử dụng dụng chmod
    1. **Phương pháp ký tự (symbolic/text)**
    
        Phương pháp ký tự thì lệnh chmod có cú pháp như sau:
        
            # chmod [OPTIONS] filename
    
        |Option|Miêu tả|
        |--------|---------|
        |``u``       |owner     |
        |``g``       |group |
        |``o``      |other
        |``a``         |all (tương đương ugo)     |
        |``x``        |execute     |
        |``w``         |write     |
        |``r``        |read     |
        |``+``        |Thêm quyền     |
        |``-``         |Xoá quyền     |
        |``=``         |Gán quyèn    |

        **Một số ví dụ về chmod sử dụng phương pháp ký tự**

        Cho phép thành viên trong group có quyền đọc file, nhưng không được ghi và thực thi:

        ``# chmod g=r filename``

        Xóa quyền thực thi đối với mọi người dùng:

        ``# chmod a-x filename``
    
        Cấp quyền đọc, ghi và thực thi cho chủ sở hữu file, cấp quyền đọc cho group và không cấp quyền nào cho mọi user khác:

        ``# chmod u=rwx, g=r, o= filename``
    
        Thêm quyền truy cập của chủ sở hữu file vào danh sách quyền của các thành viên có trong group:

        ``# chmod g+u filename``
    2. **Phương pháp số**

        Cú pháp sử dụng lệnh chmod trong Linux theo phương pháp dùng số:

            # chmod [OPTIONS] filename

        Đối với phương pháp số, ta có thể đặt quyền cập cho cả ba user class (owner, group và những user khác) cùng một lúc.

        |Option|Miêu tả|
        |--------|---------|
        |``#--``       |owner     |
        |``-#-``       |group |
        |``--#``         |other     |
        |``1``        |execute     |
        |``2``         |write     |
        |``4``        |read     |
        |``0``        |Không có quyền    |

        Ví dụ, nếu bạn muốn một tệp có quyền ``-rw-rw-rwx``, bạn sẽ sử dụng lệnh sau đây:

        |Owner|Group|Other|
        |--------|---------|---------|
        |``4+2=6``|``4+2=6``|``4+2+1=7``|

            # chmod 667 filename

        **Một số ví dụ về chmod sử dụng phương pháp số**

        Cấp quyền đọc và ghi cho chủ sở hữu file, cấp quyền chỉ đọc cho thành viên trong group và những user còn lại:

        ``# chmod 644 filename``

        Cấp quyền đọc, ghi và thực thi cho chủ sở hữu, cấp quyền đọc và thực thi cho thành viên group và không cấp quyền cho những user khác:

        ``# chmod 750 filename``

* **Quyền đặc biệt**

    Ngoài quyền truy cập thông thường (read, write, execute), còn có ba quyền đặc biệt khác trong Linux là SUID (Set User ID), SGID (Set Group ID), và Sticky Bit. Các quyền đặc biệt này được áp dụng cả cho file và thư mục.

    |Quyền|Cấu hình theo ký tự|Cấu hình theo số|
    |--------|---------|---------|
    |``SUID``|chmod +s [filename]|chmod 4XXX [filename]|
    |``SGID``|chmod +g [filename]|chmod 2XXX [filename]|
    |``Sticky bit``|chmod +t [filename]|chmod 1XXX [filename]|

    **SUID:** Được biểu thị bằng chữ 's' trong trường quyền của người dùng (ví dụ: -rwsr-xr-x).

    **SGID:** Được biểu thị bằng chữ 's' trong trường quyền của nhóm (ví dụ: -rwxr-sr-x).

    **Sticky** Bit: Được biểu thị bằng chữ 't' trong trường quyền của người khác (ví dụ: drwxrwxrwt).

    
    1. **SUID (Set User ID):**

        SUID là một quyền đặc biệt dành cho các tệp thực thi.

        Khi một tệp có SUID được thiết lập, bất kỳ người dùng nào chạy tệp đó sẽ có quyền của chủ sở hữu tệp trong quá trình thực thi.

        Ví dụ: Nếu một tệp có quyền SUID được thiết lập và tệp đó thuộc về người dùng root, bất kỳ ai chạy tệp này sẽ có quyền root trong suốt thời gian tệp được chạy.

    2. **SGID (Set Group ID):**

        SGID là một quyền đặc biệt dành cho các tệp và thư mục.

        Đối với tệp, SGID hoạt động tương tự như SUID nhưng thay vì cho người dùng quyền của chủ sở hữu tệp, nó cho người dùng quyền của nhóm chủ sở hữu tệp.
        
        Đối với thư mục, SGID đảm bảo rằng bất kỳ tệp hoặc thư mục nào được tạo ra bên trong nó sẽ kế thừa quyền nhóm của thư mục cha thay vì quyền nhóm của người tạo tệp.
    3. **Sticky Bit:**

        Sticky Bit là một quyền đặc biệt dành cho các thư mục.

        Khi Sticky Bit được thiết lập trên một thư mục, chỉ có chủ sở hữu của tệp (hoặc thư mục con), chủ sở hữu của thư mục cha hoặc người dùng root mới có thể xóa hoặc đổi tên tệp đó.

        Ví dụ phổ biến nhất của việc sử dụng Sticky Bit là thư mục /tmp, nơi nhiều người dùng có thể tạo tệp, nhưng chỉ có chủ sở hữu tệp mới có thể xóa hoặc đổi tên tệp đó.
    
* **Cách sử dụng lệnh chown để thay đổi quyền sở hữu**

    Lệnh **chown** (change owner) trong Linux được sử dụng để thay đổi chủ sở hữu và nhóm của tệp hoặc thư mục.

    Cú pháp cơ bản của lệnh chown như sau:

        # chown [OPTIONS] USER[:GROUP] FILE(s)
    
    **Trong đó:**

    * **USER**: là tên người dùng (username) hoặc ID (UID) của chủ sở hữu.

    * **GROUP**: là tên của group hoặc group ID (GID).

    * **FILE(s)**: là tên của một hay nhiều file, thư mục hoặc liên kết. Trong đó các ID dạng số phải được bắt đầu bằng ký tự +.

    **Một số ví dụ về chown:**

    * Thay đổi chủ sở hữu của tệp file.txt thành john:

        ``# chown john file.txt``
    
    * Thay đổi chủ sở hữu và nhóm của tệp file.txt thành john và developers:
    
        ``# chown john:developers file.txt``

    * Thay đổi chủ sở hữu và nhóm của thư mục project và tất cả các tệp, thư mục con bên trong nó thành john và developers:
    
        ``# chown -R john:developers project``
    
    * Đổi chủ sở hữu bằng file tham chiếu;

        Option `--reference=ref_file` cho phép ta thay đổi quyền sở hữu theo user và group của các file dựa trên quyền sở hữu của file tham chiếu được chỉ định trong `ref_file`. Nếu file tham chiếu là một liên kết tượng trưng thì chown sẽ sử dụng user và group của file đích.

        ``# chown --reference=REF_FILE FILE``

        ``# chown --reference=reference.txt file.txt``

## III.  Nén và giải nén tập tin

### Các loại nén và giải nén

* **Gzip**

    Gzip nén kích thước của các tập tin cho trước bằng cách sử dụng mã hóa Lempel-Ziv (LZ77). Khi có thể, mỗi tập tin sẽ được thay thế bằng một tập tin có phần mở rộng .gz. 

    * **Cú pháp nén:** ``gzip {filename}``

    * **Cú pháp giải nén:** ``gzip -d {.gz file}`` hoặc ``gunzip {.gz file}``

    * **Ví dụ:**
        
        ``gzip mydata.doc``

        ``gzip *.jpg``

        ``gzip -d mydata.doc.gz``

        ``gunzip mydata.doc.gz``

* **Bzip2**

    Bzip2 nén các tệp bằng thuật toán nén văn bản sắp xếp khối Burrows-Wheeler và mã hóa Huffman. Nén thông thường được cải thiện đáng kể so với các bộ nén dựa trên LZ77/LZ78 như lệnh bzip. Khi có thể, mỗi tệp sẽ được thay thế bằng một tệp có phần mở rộng .bz2.

    * **Cú pháp nén:** ``bzip2 {filename}``

    * **Cú pháp nén:** ``bzip2 -d {.bz2-file}`` hoặc ``bunzip2 {.bz2-file}``

    * **Ví dụ:**
        
        ``bzip2 mydata.doc``

        ``bzip2 *.jpg``

        ``bzip2 -d mydata.doc.bz2``

        ``gunzip mydata.doc.bz2``
* **Zip** 
    
    Là một tiện ích nén và đóng gói tệp tin cho Unix/Linux. Mỗi tệp tin được lưu trữ trong một tệp .zip duy nhất với phần mở rộng .zip.

    * **Cú pháp nén:** ``zip {.zip-filename} {filename-to-compress}``

    * **Cú pháp giải nén:** ``unzip {.zip file}``
    
    * **Ví dụ:**
        
        ``zip mydata.zip mydata.doc``

        ``zip data.zip *.doc``

        ``unzip file.zip``
        
        ``unzip data.zip resume.doc``
    
* **Tar**

    GNU tar là một tiện ích dùng để lưu trữ các tệp tin nhưng cũng có thể được sử dụng để nén các tệp tin lớn. GNU tar hỗ trợ cả nén lưu trữ thông qua gzip và bzip2. Nếu bạn có nhiều hơn 2 tệp tin, thì nên sử dụng tar thay vì gzip hoặc bzip2.

    * **Cú pháp chung:**    ``tar [options] [file archive] [thư mục hoặc directory cần lưu trữ]``
    
        | Option | Description                                      |
        |--------|--------------------------------------------------|
        | ``-c``     | Tạo Archive.                                     |
        | ``-x``     | Giải nén archive.                                |
        | ``-f``     | Tạo archive với tên file được xác định sẵn.     |
        | ``-t``     | Liệt kê các file trong archive.                  |
        | ``-u``     | Tạo archive rồi thêm vào file archive có sẵn.   |
        | ``-v``     | Hiển thị thông tin đầy đủ (verbose).            |
        | ``-a``     | Nối các file archive.                            |
        | ``-z``     | Zip, yêu cầu tạo file tar bằng gzip.             |
        | ``-j``     | Lọc archive bằng tbzip.                          |
        | ``-w``     | Xác thực file archive.                           |
        | ``-r``     | Thêm hoặc cập nhật file, thư mục trong file .tar có sẵn. |
    
    * **Ví dụ:**
      1. **Lệnh nén**
      
            ``tar -zcvf data.tgz *.doc``

            ``tar -zcvf pics.tar.gz *.jpg *.png``

            ``tar -jcvf data.tbz2 *.doc``
    
      2. **Lệnh giải nén**
   
            ``tar -zxvf data.tgz``

            ``tar -zxvf pics.tar.gz *.jpg``

            ``tar -jxvf data.tbz2``

# END