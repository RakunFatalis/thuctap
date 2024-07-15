# WORKING WITH FILE

# MỤC LỤC

- [WORKING WITH FILE](#working-with-file)
- [MỤC LỤC](#mục-lục)
- [LỜI MỞ ĐẦU](#lời-mở-đầu)
  - [Xác định các thư mục và file với lệnh ls](#xác-định-các-thư-mục-và-file-với-lệnh-ls)
  - [Hiển thị nội dung file với lệnh cat](#hiển-thị-nội-dung-file-với-lệnh-cat)
  - [Xem nội dung file với lệnh less và lệnh more](#xem-nội-dung-file-với-lệnh-less-và-lệnh-more)
  - [Xem nhanh nội dung các dòng của file với lệnh head and tail](#xem-nhanh-nội-dung-các-dòng-của-file-với-lệnh-head-and-tail)
  - [Soạn thảo văn bản với vi/vim](#soạn-thảo-văn-bản-với-vivim)
  - [Xử lý và phân tích văn bản cấu trúc với lệnh awk](#xử-lý-và-phân-tích-văn-bản-cấu-trúc-với-lệnh-awk)
  - [Theo dõi tiến trình của hệ thống bằng lệnh ps](#theo-dõi-tiến-trình-của-hệ-thống-bằng-lệnh-ps)
  - [Truy vấn thông tin DNS với lệnh dig](#truy-vấn-thông-tin-dns-với-lệnh-dig)
  - [Xử lý và phân tích văn bản với các lệnh tr, tee, wc, cut](#xử-lý-và-phân-tích-văn-bản-với-các-lệnh-tr-tee-wc-cut)
  - [Tìm kiếm và phân tích văn bản với lệnh grep](#tìm-kiếm-và-phân-tích-văn-bản-với-lệnh-grep)
  - [Chỉnh sửa dữ liệu với lệnh sed](#chỉnh-sửa-dữ-liệu-với-lệnh-sed)
- [END](#end)


# LỜI MỞ ĐẦU

Linux là một hệ điều hành mạnh mẽ và linh hoạt, được sử dụng rộng rãi trong các hệ thống máy tính cá nhân, máy chủ và các thiết bị nhúng. Một trong những kỹ năng quan trọng và cơ bản khi làm việc với Linux là quản lý và thao tác với các file. Khả năng xử lý file hiệu quả không chỉ giúp bạn tổ chức dữ liệu một cách khoa học mà còn nâng cao năng suất làm việc và giảm thiểu các lỗi phát sinh.

Trong môi trường Linux, mọi thứ đều được biểu diễn dưới dạng file, từ các tập tin văn bản, hình ảnh cho đến các thiết bị phần cứng như ổ đĩa và cổng mạng. Việc hiểu rõ cấu trúc hệ thống file, các lệnh cơ bản để thao tác với file và quyền truy cập là nền tảng để bạn có thể khai thác hết sức mạnh của hệ điều hành này.

Trong bài viết này, chúng ta sẽ cùng khám phá các khía cạnh cơ bản của làm việc với file trong Linux. Từ việc tạo mới, sao chép, di chuyển, đổi tên đến việc thay đổi quyền truy cập và xem thông tin chi tiết của các file và thư mục. Qua đó, bạn sẽ có cái nhìn tổng quan và nắm bắt được những kỹ năng cần thiết để làm việc một cách hiệu quả trong môi trường Linux.

## Xác định các thư mục và file với lệnh ls

Lệnh ``ls`` được sử dụng để liệt kê tất cả các tệp và folder có trong thư mục (directory) làm việc hiện tại của bạn. Bạn cũng có thể nhận được nhiều thông tin về các tệp bằng cách sử dụng cùng một lệnh. Vì nó đã được bao gồm trong gói tiện ích cốt lõi GNU, bạn không cần phải cài đặt thêm bất kỳ gói nào trên hệ thống của mình để sử dụng nó.

Cú pháp cơ bản với lệnh ls:

``# ls [option] [directory]``

Các tuỳ chọn của lệnh ls:

| Tuỳ chọn   | Mô tả                                                                                  |
|--------|---------------------------------------------------------------------------------------------|
| `-l`| Liệt kê các tệp và thư mục với thông tin chi tiết.                         |
| `-a`| Hiển thị tất cả các tệp, bao gồm các tệp ẩn.                      |
| `-F`| Hiển thị loại tệp.             |
| `-R`| Liệt kê đệ quy tất cả các tệp và thư mục con.                                               |
| `-t`| Sắp xếp các tệp theo thời gian sửa đổi gần nhất.                                            |
| `-r`| Sắp xếp các tệp theo thứ tự ngược lại.                                  |
| `-s`| Hiển thị kích thước của tệp.                                             |
| `-h`| Hiển thị kích thước của tệp theo định dạng dễ đọc hơn (KB, MB, GB, v.v.) khi sử dụng cùng với `-l` hoặc `-s`. |


Ví dụ:

Chúng ta muốn hiển thị thông tin chi tiết từ quyền, người sở hữu, ngày tạo của file thì dùng câu lệnh:

``# ls -l``

![](/thuctap/img/ls-l.png)


## Hiển thị nội dung file với lệnh cat

Lệnh này được sử dụng để nối và hiển thị nội dung của các tệp. Tuy nhiên, một hạn chế của ``cat`` là khi in ra nội dung của file thì nếu file quá dài ta không thể xem hết được, mà buộc phải kết hợp với các câu lệnh khác.

Các lệnh `cat` phổ biến

| Lệnh            | Ý nghĩa                                                                   |
|-----------------|---------------------------------------------------------------------------|
| `cat filename`  | Hiển thị nội dung của tệp `filename`.                                     |
| `cat file1 file2`| Nối và hiển thị nội dung của tệp `file1` và `file2`.                     |
| `cat > filename`| Tạo tệp mới `filename` và cho phép nhập nội dung (kết thúc bằng Ctrl+D). |
| `cat >> filename`| Thêm nội dung vào cuối tệp `filename` (kết thúc bằng Ctrl+D).            |
| `cat -n filename`| Hiển thị nội dung của tệp `filename` với số dòng.                        |
| `cat -b filename`| Hiển thị nội dung của tệp `filename` với số dòng nhưng bỏ qua các dòng trống.|
| `cat -s filename`| Nén nhiều dòng trống liên tiếp thành một dòng trống duy nhất.            |
| `cat -E filename`| Hiển thị dấu `$` ở cuối mỗi dòng.                                        |

Ví dụ: Muốn xem thông tin của một file:

![](/thuctap/img/catfile1.png)


## Xem nội dung file với lệnh less và lệnh more

Khác với lệnh ``cat`` hiển thị toàn bộ nội dung của tệp trong một lần và khi một file quá lớn thì không thể xem hết được. Vì thế lệnh ``less`` và lệnh ``more`` được sinh ra để khắc phục điểm yếu của lệnh ``cat``. Cả hai lệnh đều có điểm chung là hiện thị thông tin của file mà không cần tới trình soạn thảo, có thể tìm kiếm trong file và điều hướng của trang.

* **Lệnh less**

    Cú pháp cơ bản: ``# less [file_name]``

    **Phím điều hướng trong `less`**

    | Phím               | Ý nghĩa                                   |
    |--------------------|-------------------------------------------|
    | `Space`            | Chuyển đến trang tiếp theo.               |
    | `b`                | Quay lại trang trước.                     |
    | `G`                | Chuyển đến cuối tệp.                      |
    | `g`                | Chuyển đến đầu tệp.                       |
    | `/pattern`         | Tìm kiếm từ `pattern` trong tệp.          |
    | `n`                | Chuyển đến kết quả tìm kiếm tiếp theo.    |
    | `N`                | Chuyển đến kết quả tìm kiếm trước đó.     |
    | `q`                | Thoát khỏi `less`.                        |

* **Lệnh more**

    Cú pháp cơ bản: ``# more [file_name]``

    **Phím điều hướng trong `more`**

    | Phím               | Ý nghĩa                                   |
    |--------------------|-------------------------------------------|
    | `Space`            | Chuyển đến trang tiếp theo.               |
    | `Enter`            | Chuyển xuống dòng tiếp theo.              |
    | `b`                | Quay lại trang trước (nếu được hỗ trợ).   |
    | `/pattern`         | Tìm kiếm từ `pattern` trong tệp.          |
    | `q`                | Thoát khỏi `more`.                        |

Khi nào sử dụng mỗi lệnh:

``cat:`` Khi bạn cần nhanh chóng xem nội dung của tệp nhỏ hoặc nối nhiều tệp và hiển thị chúng.

``less:`` Khi bạn cần xem tệp lớn và điều hướng linh hoạt, cuộn lên/xuống, và tìm kiếm trong tệp.

``more:`` Khi bạn cần xem tệp lớn theo trang và không cần cuộn lên hoặc các tính năng điều hướng phức tạp.

## Xem nhanh nội dung các dòng của file với lệnh head and tail

* **Lệnh head**

    Lệnh ``head`` được sử dụng để hiển thị nội dung của các dòng đầu tiên của một tệp văn bản.

    Cú pháp cơ bản: ``# head filename``

    Các tùy chọn thường được sử dụng với head:

    ``-n N``: Hiển thị N dòng đầu tiên của tệp (mặc định là 10 dòng).

    Ví dụ: ``# head -n 20 filename``   # Hiển thị 20 dòng đầu tiên của `filename`

* **Lệnh tail**

    Lệnh ``tail`` được sử dụng để hiển thị nội dung của các dòng cuối cùng của một tệp văn bản.

    Cú pháp cơ bản: ``# tail filename``

    Các tùy chọn thường được sử dụng với tail:

    ``-n N``: Hiển thị N dòng cuối cùng của tệp (mặc định là 10 dòng).

    ``-f``: Theo dõi thêm nội dung của tệp. Lệnh sẽ không kết thúc và sẽ hiển thị dòng mới khi được thêm vào tệp.

    Ví dụ:

    ``# tail -n 30 filename``   # Hiển thị 30 dòng cuối cùng của `filename`

    ``# tail -f filename``     # Theo dõi thêm nội dung của `filename`

## Soạn thảo văn bản với vi/vim

``vi`` và ``vim`` là hai trình soạn thảo văn bản phổ biến trên các hệ điều hành Unix/Linux. Trong thực tế, ``vim`` là phiên bản cải tiến của ``vi`` với nhiều tính năng hơn và được sử dụng rộng rãi hơn.

* **Cách sử dụng cơ bản vi/vim**

    **Mở một tệp:** ``# vi filename`` hoặc # ``vim filename``

    Nếu ``filename`` không tồn tại, vi sẽ tạo một tệp mới với tên đó.

    **Chuyển giữa các chế độ:**
    
    ``i``: Chế độ chỉnh sửa.

    ``Esc``: Chế độ lệnh.

    **Lưu và thoát:**

    Trong chế độ lệnh, nhập ``:w`` để lưu tệp.

    Nhập ``:q`` để thoát.

    Kết hợp ``:wq`` để lưu và thoát.

* **Các lệnh trong chế độ chỉnh sửa**

    **Các lệnh di chuyển**

    | Phím               | Ý nghĩa                                   |
    |--------------------|-------------------------------------------|
    | `Các phím mũi tên (↑, ↓, ←, →)`| Để di chuyển con trỏ.         |
    | `Ctrl + f`         | Để cuộn trang xuống.                      |
    | `Ctrl + b`         | Để cuộn trang lên.                        |
    | `gg`               | Để di chuyển tới đầu tệp                 |
    | `G`                | để di chuyển tới cuối tệp.                |

    **Các lệnh xử lý văn bản**

    | Phím               | Ý nghĩa                                   |
    |--------------------|-------------------------------------------|
    | `x                `| Để xóa ký tự hiện tại         |
    | `dw`               | Để xóa từ hiện tại                      |
    | `d$`               | Để xóa từ vị trí hiện tại tới cuối dòng.                        |
    | `:/pattern`        | Để tìm kiếm                |

    Ngoài ra còn có rất nhiều câu lệnh khác nữa, muốn biết thêm chi tiết các bạn vào link này để biết các lệnh trong trình soạn thảo vi/vim

    [Vi/Vim Cheat Sheet](https://vim.rtorr.com/)
* **So sánh vi và vim**

``vi`` là phiên bản gốc có sẵn trên hầu hết các hệ điều hành Unix/Linux, trong khi vim là phiên bản mở rộng và cải tiến hơn.

``vim`` có nhiều tính năng hơn, bao gồm cả cú pháp màu, hỗ trợ plugin, và các chế độ mở rộng.

Cả ``vi`` và ``vim`` đều có các phím tắt và cách sử dụng tương tự, nhưng vim có thêm nhiều tính năng và linh hoạt hơn để chỉnh sửa và quản lý tệp văn bản.


## Xử lý và phân tích văn bản cấu trúc với lệnh awk

Lệnh ``awk`` là một công cụ mạnh mẽ trong Unix và các hệ điều hành tương tự, được sử dụng để xử lý và phân tích văn bản cấu trúc. Awk có thể sử dụng để thực hiện các phép lọc, biến đổi và định dạng lại dữ liệu từ các tệp văn bản.

**Cách hoạt động của awk:**

Lệnh awk được thiết kế để giúp việc truy xuất thông tin và xử lý văn bản trở nên dễ dàng trên môi trường Unix và Linux. Chức năng chính của awk là quét qua các dòng dữ liệu đầu vào, tìm kiếm các dòng phù hợp với các mẫu mà người dùng chỉ định.

Đối với ``pattern``, người dùng có thể chỉ định một hành động để thực hiện trên mỗi dòng phù hợp với mẫu đã chỉ định. Nhờ vào awk, người dùng có thể dễ dàng xử lý các tệp log phức tạp và tạo ra các báo cáo dễ đọc được.

**Các hoạt động của awk**

* Quét một tệp từng dòng một.
* Chia dòng/văn bản đầu vào thành các trường (fields).
* So sánh dòng đầu vào hoặc các trường với các mẫu được chỉ định.
* Thực hiện các hành động khác nhau trên các dòng phù hợp.
* Định dạng các dòng đầu ra.
* Thực hiện các phép tính số học và thao tác chuỗi.
* Sử dụng luồng điều khiển và vòng lặp trên đầu ra.
* Biến đổi các tệp và dữ liệu theo một cấu trúc đã chỉ định.
* Tạo ra các báo cáo được định dạng.
* awk là một công cụ rất mạnh mẽ trong Unix và Linux, giúp người dùng xử lý và biến đổi dữ liệu văn bản một cách linh hoạt và hiệu quả.


**Cú pháp cơ bản:** ``# awk 'pattern { action }' filename``

* Trong đó:

    **pattern:** Điều kiện để thực hiện hành động. Nếu không có điều kiện, hành động sẽ được thực hiện cho mỗi dòng của tệp.

    **{ action }:** Hành động được thực hiện khi pattern được thỏa mãn.

    **filename:** File cần thực hiện lệnh awk.

**Ví dụ:**

Giả sử ta có một tệp ``hoadon.txt`` như sau:

![](/thuctap//img/hoadon.txt.png)


Để hiển thị cột thứ 2 (cột Fruit), bạn có thể sử dụng awk như sau:

``# awk '{ print $2 }' hoadon.txt``

![](/thuctap/img/awk_print$2.png)

Để tính toán trung bình của cột "Total Amount", bạn có thể sử dụng awk như sau:

``# awk '{ sum+=$5} END { print sum/NR}' hoadon.txt``

![](/thuctap/img/awk_sumNR.png)

Chúng ta còn có thể in ra nội dung dựa vào việc ta lọc số dòng, ví dụ ta muốn in dòng có chứa thông tin STT 3 ta dùng câu lệnh sau:

``# awk 'NR==7' hoadon.txt``

![](/thuctap/img/awk_NR7.png)

Để hiểu rõ hơn về lệnh awk các bạn có thể đọc các tài liệu sau đây:

https://www.geeksforgeeks.org/awk-command-unixlinux-examples/

https://manpages.ubuntu.com/manpages/trusty/man1/awk.1posix.html


## Theo dõi tiến trình của hệ thống bằng lệnh ps

Lệnh ``ps``, viết tắt của "process status", là một công cụ giúp bạn xem những gì đang diễn ra bên trong máy tính Linux của bạn. Hãy tưởng tượng máy tính của bạn đồng thời đang thực hiện nhiều công việc khác nhau, như chạy các chương trình hoặc ứng dụng khác nhau. Những công việc này được gọi là các quá trình và lệnh ps cho phép bạn nhìn nhanh vào chúng. Khi bạn sử dụng nó mà không có bất kỳ hướng dẫn đặc biệt nào, nó sẽ hiển thị các quá trình liên kết với cửa sổ hoặc màn hình mà bạn đang sử dụng.

**Cú pháp cơ bản:** ``# ps [options]``

Các tuỳ chọn phổ biến trong lệnh ps

| Tùy chọn | Mô tả |
|----------|------|
| `-A`, `-e` | Liệt kê tất cả các quá trình đang chạy trên toàn hệ thống|
| `-a` | Liệt kê tất cả các quá trình ngoại trừ các lãnh đạo phiên (trường hợp mã quá trình giống với mã ID phiên) và các quá trình không liên quan đến một thiết bị đầu cuối. |
| `-d` | Liệt kê tất cả các quá trình ngoại trừ các lãnh đạo phiên, cung cấp một cái nhìn lọc thông tin về các quá trình đang chạy trên hệ thống. |
| `--deselect`, `-N` | Liệt kê tất cả các quá trình ngoại trừ những quá trình đáp ứng các điều kiện được định nghĩa bởi người dùng. |
| `-f` | Hiển thị cấu trúc phân cấp của các quá trình dưới dạng đồ họa ASCII, minh họa mối quan hệ cha con giữa chúng. |
| `-j` | Hiển thị đầu ra dưới dạng công việc, cung cấp thông tin chi tiết như process ID, session ID, và lệnh. |
| `-T` | Liệt kê tất cả các quá trình liên quan đến thiết bị đầu cuối hiện tại, hỗ trợ tập trung vào các nhiệm vụ liên quan đến một phiên bản terminal cụ thể. |
| `-r` | Chỉ liệt kê các quá trình đang chạy, hữu ích cho việc theo dõi hiệu suất hệ thống. |
| `-u` | Mở rộng đầu ra để bao gồm thông tin bổ sung như sử dụng CPU và bộ nhớ. |
| `-u` | Chỉ định một tên người dùng, liệt kê các quá trình liên quan đến người dùng đó. |
| `-x` | Bao gồm các quá trình không có TTY, hiển thị các quá trình nền không liên quan đến một phiên bản terminal cụ thể. |

**Ví dụ:**
    
* Khi chúng ta thực hiện lệnh ps mà không có bất kỳ đối số nào, nó sẽ hiển thị các tiến trình trong Shell hiện tại.

    ![](/thuctap/img/ps.png)

    **Trong đó:**

    ``PID``: ID.

    ``TTY``: Tiến trình duy nhất, loại thiết bị đầu cuối mà người dùng đã đăng nhập vào.

    ``TIME``: số lượng CPU tính bằng phút và giây mà tiến trình đã chạy.

    ``CMD``: Tên của lệnh đã khởi chạy tiến trình.

Để hiển thị mọi tiến trình hoạt động trên hệ thống Linux ở định dạng BSD chúng ta có thể sử dụng tùy chọn au hoặc tùy chọn axu, hai tuỳ chọn này tương đương nhau như sau:

![](/thuctap/img/ps_au.png)


## Truy vấn thông tin DNS với lệnh dig

Lệnh ``dig`` là một công cụ dòng lệnh trong Linux được sử dụng để thực hiện các truy vấn DNS (Domain Name System). Nó cung cấp khả năng kiểm tra và truy xuất thông tin DNS từ các máy chủ DNS.

* **Cài đặt lệnh dig:**

    Để kiểm tra xem lệnh ``dig`` có trên hệ thống của chúng ta không ta sử dụng lệnh sau:

    ``# dig -v``

    ![](/thuctap/img/dig_v.png)

    Nếu không có ta sử dụng lệnh sau để cài đặt:

  * Đối với Ubuntu/Debiam:
  
    ``# apt install dnsutils``

  * Đối với CentOS/RHEL:

    ``# yum install bind-utils``


* **Cú pháp cơ bản lệnh dig:**

    ``# dig [server] [name] [type]``

    **Trong đó:**

    ``[server]``: Tên máy chủ hoặc địa chỉ IP mà truy vấn được hướng tới.

    ``[name]``: Tên miền DNS của máy chủ để truy vấn.

    ``[type]``: Loại bản ghi DNS để truy xuất. Mặc định (hoặc nếu để trống), dig sẽ sử dụng loại bản ghi A.

* **các tuỳ chọn phổ biến trong lệnh dig:**

| Tùy chọn | Mô tả |
|---------------------------------------------------|------|
| `MX` | Truy vấn bản ghi MX của tên miền, hiển thị các máy chủ thư điện tử. |
| `NS` | Truy vấn bản ghi NS của tên miền, hiển thị các máy chủ DNS chính. |
| `TXT`| Truy vấn bản ghi TXT của tên miền, hiển thị thông tin phụ trợ. |
| `-x` | Truy vấn ngược để tìm tên miền (PTR record) cho địa chỉ IP.|
| `+noall +answer example.com`| Hiển thị chỉ các câu trả lời cụ thể cho tên miền. |
| `@dns-server example.com`   | Sử dụng máy chủ DNS cụ thể (`dns-server`) để thực hiện truy vấn cho tên miền. |
| `+nocmd +noquestion +nocomments +nostats +noclass +noadditional +noauthority +nosoa example.com` | Hiển thị đầy đủ thông tin về bản ghi SOA của tên miền `example.com`. |

**Ví dụ:**

Truy vấn DNS cơ bản, tại ví dụ này ta truy vấn thông tin tên miền ``google.com``

![](/thuctap/img/dig_google.png)

Truy vấn địa chỉ IP, tại ví dụ này ta thử truy vấn địa chỉ IP của tên miền ``amazon.com``

![](/thuctap/img/dig_amazon_short.png)

Tra cứu DNS ngược, tại ví dụ này ta thử tra cứu DNS của địa chỉ IP ``17.253.144.10``

``# dig -x 17.253.144.10``, nó sẽ hiện ra DNS của IP này là của Apple

![](/thuctap/img/dig_x_apple.png)

## Xử lý và phân tích văn bản với các lệnh tr, tee, wc, cut

* **Lệnh tr**

    Lệnh ``tr`` trong Linux được sử dụng để thay đổi hoặc xóa các ký tự từ input stream

    Cú pháp cơ bản: tr [OPTIONS] SET1 [SET2]

    Trong đó:
    
    * SET1: Chuỗi các ký tự muốn thay đổi hoặc loại bỏ.
    
    * SET2: Chuỗi các ký tự mới để thay thế, hoặc không có nếu chỉ muốn xóa.

    **Ví dụ**

    Thay đổi hoặc xóa ký tự từ input

    ![](/thuctap/img/tr_aA.png)

    Xóa ký tự khoảng trắng từ input

    ![](/thuctap/img/tr_space.png)

    Đổi chữ thường thành chữ hoa

    ![](/thuctap/img/tr_upper.png)

* **Lệnh tee**

    Lệnh ``tee`` trong Linux được sử dụng để đọc từ standard input và ghi đồng thời vào standard output và các tệp tin được chỉ định.

    Cú pháp cơ bản: ``# tee [OPTIONS] [file_name]``

    | Tùy chọn | Mô tả |
    |---------------------------------------------------|------|
    | `-a` | Ghi dữ liệu vào cuối tệp tin thay vì ghi đè lên nếu tệp tin đã tồn tại. |
    | `-i` | Bỏ qua tín hiệu gián đoạn (interrupt signals), giúp giữ nguyên quá trình ghi khi có tín hiệu SIGINT. |
    | `--help`| Hiển thị trợ giúp về các tùy chọn của lệnh ``tee``. |
    | `--version` | Hiển thị thông tin về phiên bản của ``tee``|

    **Ví dụ**

    * **Ghi đồng thời vào standard output và tệp tin**

        ![](/thuctap/img/tee_hello.png)

        Lệnh này sẽ ghi "Hello, world!" vào hello.txt và hiển thị nội dung đó trên standard output.

    * **Thêm nội dung vào cuối tệp tin (append)**

        ![](/thuctap/img/tee_a_redandblue.png)

        Lệnh này sẽ thêm "Red and Blue" vào cuối hello.txt mà không ghi đè lên nội dung đã có.

* **Lệnh wc**

    Lệnh ``wc`` trong Linux là một công cụ để đếm số dòng, số từ, số byte và các thống kê khác của các tệp văn bản được chỉ định hoặc đầu vào từ standard input.

    Cú pháp cơ bản: ``# wc [OPTIONS] [file_name]``

    | Tùy chọn | Mô tả |
    |---------------------------------------------------|------|
    | `-l` | Đếm số dòng. |
    | `-w` | Đếm số từ.|
    | `-c` | Đếm số byte. |
    | `-m` | Đếm số ký tự|

    **Ví dụ:**

    * **Đếm số dòng trong một tệp tin**

        ``# wc -l hoadon.txt``

        ![](/thuctap/img/wc_l.png)

    * **Đếm số từ trong đầu vào từ standard input**

        ``# echo "This is a test" | wc -w``

        ![](/thuctap/img/wc_w.png)

    * **Đếm số byte trong một tệp tin**

        ``# wc -c hoadon.txt``

        ![](/thuctap/img/wc_c.png)

    * **Kết hợp đếm số dòng, số từ và số byte trong một tệp tin**

        ``# wc -l -w -c hoadon.txt``

        ![](/thuctap/img/wc_lwc.png)

* **Lệnh cut**

    Lệnh ``cut`` trong Linux là một công cụ dòng lệnh được sử dụng để trích xuất các phần cụ thể của mỗi dòng từ một tệp hoặc từ đầu vào standard input.

    Cú pháp cơ bản: ``# cut [OPTIONS] [FILE...]``

    | Tùy chọn | Mô tả |
    |---------------------------------------------------|------|
    | `-b` | Chọn các byte được chỉ định trong danh sách. |
    | `-c` | Chọn các ký tự được chỉ định trong danh sách.|
    | `-d` | Sử dụng ký tự DELIM làm delimiter (dấu phân cách) thay vì dấu tab mặc định.. |
    | `-f` | Chọn các trường được chỉ định trong danh sách (dựa trên delimiter)|
    | `-n`  | Chọn các byte, ký tự hoặc trường ngoài danh sách|

    * **Ví dụ**

    * **Cắt bỏ từ ký tự thứ 3 đến cuối mỗi dòng**

        ``# cut -c 3- rose.txt``

        ![](/thuctap/img/cut-c3-.png)

    * **Cắt các byte thứ 1, 4 và 7 từ mỗi dòng:**

        ``# echo "abcdefgh" | cut -b1,4,7``

        ![](/thuctap/img/cut_b147.png)

## Tìm kiếm và phân tích văn bản với lệnh grep

Lệnh ``grep`` trong Linux là một công cụ mạnh mẽ để tìm kiếm văn bản trong các tệp hoặc đầu vào dòng lệnh.

* **Cú pháp cơ bản lệnh grep**

    ``# grep [OPTIONS] PATTERN [file_name]``

    **Các tuỳ chọn phổ biến của lệnh grep**

    | Tùy chọn          | Mô tả                                                                 |
    |-------------------|----------------------------------------------------------------------|
    | `-i`| Bỏ qua phân biệt chữ hoa và chữ thường khi tìm kiếm.              |
    | `-v`| Chỉ hiển thị các dòng không chứa mẫu tìm kiếm.                   |
    | `-c`| Đếm số dòng chứa mẫu tìm kiếm và chỉ hiển thị số lượng này.      |
    | `-l`| Chỉ hiển thị tên tệp chứa mẫu tìm kiếm.                         |
    | `-n`| Hiển thị số dòng của các dòng chứa mẫu tìm kiếm.                 |
    | `-H`| Hiển thị tên tệp cùng với các dòng chứa mẫu tìm kiếm.            |
    | `-r`| Tìm kiếm đệ quy trong các thư mục con.

    Gõ lệnh: ``# man grep`` để biết thêm các tuỳ chọn khác

* **Ví dụ**

    **Tìm kiếm một từ trong một tệp**

    ``# grep "Violet" rose.txt``

    ![](/thuctap/img/grep_violat.png)

    **Tìm kiếm không phân biệt chữ hoa chữ thường**

    ``# grep -i "ARE" rose.txt``

    ![](/thuctap/img/grep_ARE.png)

    **Đếm số dòng chứa mẫu tìm kiếm**

    ``# grep -c "are" rose.txt``

    ![](/thuctap/img/grep_c_rose.png)

    **Hiển thị số dòng chứa mẫu tìm kiếm**

    ``# grep -n "are" rose.txt``

    ![](/thuctap/img/grep_n.png)

## Chỉnh sửa dữ liệu với lệnh sed

Lệnh ``sed`` (stream editor) trong Linux là một công cụ mạnh mẽ để xử lý và chuyển đổi văn bản. Nó được sử dụng để chỉnh sửa dữ liệu trong một tệp hoặc dòng đầu vào mà không cần mở tệp trong một trình soạn thảo văn bản.

* **Cú pháp cơ bản trong lệnh sed**

    ``# sed [OPTIONS] 'script' [file_name]``

    | Tùy chọn                      | Mô tả                 |
    |-------------------------------|-----------------------|
    | `-e script` | Chỉ định script để thựchiện.                                                        |
    | `-f script-file`| Đọc các script từ một tệp.                                                        |
    | `-i[SUFFIX]` | Chỉnh sửa tệp tại chỗ (cập nhật tệp gốc).                                            |
    | `-n, --quiet, --silent`       | Ức chế đầu ra mặc định; chỉ in những dòng được chỉ định bởi các lệnh `p`.              |
    | `-r`       | Sử dụng biểu thức chính quy mở rộng.                                                  |

    | Script                       | Mô tả                         |
    |----------------------------|-------------------------------|
    | `s/pattern/replacement/[flags]` | Thay thế `pattern` bằng `replacement`.                                               |
    | `d`                        | Xóa các dòng khớp với mẫu.     |
    | `p`                        | In các dòng khớp với mẫu.       |
    | `a\ text`                  | Thêm `text` sau dòng khớp với mẫu.|
    | `i\ text`                  | Chèn `text` trước dòng khớp với mẫu.|

    * **Ví dụ**
    
    **Thay thế chuỗi văn bản trong một tệp**

    ``# sed 's/Roses/roses/g' file.txt``

    ![](/thuctap/img/sed_rose.png)

    **Xóa các dòng chứa một chuỗi cụ thể**

    ``# sed '/are/d' rose.txt``

    ![](/thuctap/img/sed_are.png)

    **In các dòng khớp với mẫu**

    `# sed -n '/are/p' rose.txt`

    ![](/thuctap/img/sed_n_are.png)

# END

