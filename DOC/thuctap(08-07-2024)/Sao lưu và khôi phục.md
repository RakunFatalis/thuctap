# SAO LƯU VÀ KHÔI PHỤC

# MỤC LỤC

- [SAO LƯU VÀ KHÔI PHỤC](#sao-lưu-và-khôi-phục)
- [MỤC LỤC](#mục-lục)
  - [I. Sao lưu dữ liệu](#i-sao-lưu-dữ-liệu)
    - [1. Sao lưu tập tin và hệ thống](#1-sao-lưu-tập-tin-và-hệ-thống)
      - [A. Lệnh Rsync](#a-lệnh-rsync)
      - [B. Lệnh Tar](#b-lệnh-tar)
    - [2. Cấu hình sao lưu định kỳ với Cron jobs](#2-cấu-hình-sao-lưu-định-kỳ-với-cron-jobs)
  - [II. Khôi phục dữ liệu](#ii-khôi-phục-dữ-liệu)
- [END](#end)

## I. Sao lưu dữ liệu

### 1. Sao lưu tập tin và hệ thống

#### A. Lệnh Rsync

Rsync (Remote Sync) là lệnh được sử dụng phổ biến để sao chép và đồng bộ hóa các tệp, thư mục từ xa cũng như cục bộ trong các hệ thống Linux/Unix.

Với sự trợ giúp của lệnh rsync, có thể sao chép và đồng bộ dữ liệu từ xa và nội bộ trên các thư mục, ổ đĩa và mạng, thực hiện sao lưu dữ liệu và nhân bản giữa hai máy chủ Linux.

Cú pháp lệnh Rsync: 

``# rsync [options] source destination``

Trong đó:
* ``SOURCE`` chỉ định (các) tệp hoặc thư mục nguồn sẽ được chuyển, có thể là vị trí cục bộ hoặc vị trí từ xa.
* ``DESTINATION`` chỉ định đường dẫn đích nơi các tệp hoặc thư mục sẽ được sao chép. Tương tư như Source, nó có thể là đường dẫn cục bộ

Các tùy chọn dùng với lệnh rsync

| Option | Mô tả |
|-------------|------------------------------------------------------------|
| `-v`        | Verbose output, hiển thị thông tin chi tiết về quá trình xử lí chuyển dữ liệu |
| `-r`        | Sao chép dữ liệu theo cách đệ quy, không lưu giữ dấu thời gian và quyền trong khi chuyển dữ liệu |
| `-a`        | Chế độ lưu trữ, sao chép tệp đệ quy và duy trì các liên kết tượng trưng, quyền truy cập tệp, quyền sở hữu của người dùng và nhóm cũng như dấu thời gian |
| `-z`        | Nén tệp trong khi chuyển để giảm mức sử dụng mạng |
| `-h`        | Người dùng có thể đọc, in ra số ở định dạng người có thể đọc được |
| `-P`        | Hiển thị tiến độ trong quá trình chuyển |

#### B. Lệnh Tar

Lệnh Tar là một tiện ích dùng để lưu trữ các tệp tin nhưng cũng có thể được sử dụng để nén các tệp tin lớn. GNU tar hỗ trợ cả nén lưu trữ thông qua gzip và bzip2. Nếu bạn có nhiều hơn 2 tệp tin, thì nên sử dụng tar thay vì gzip hoặc bzip2.

Cú pháp lệnh:

``# tar [options] [file archive] [thư mục hoặc directory cần lưu trữ]``

Các tùy chọn dùng với lệnh tar

| Option | Mô tả                                      |
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


### 2. Cấu hình sao lưu định kỳ với Cron jobs

Cron jobs là một cơ chế trong hệ điều hành Unix và các hệ điều hành tương tự như Linux, được sử dụng để lên lịch thực hiện các công việc tự động vào các thời điểm cụ thể. "Cron" là một tiện ích quản lý thời gian trong Unix, cho phép người dùng thiết lập và quản lý các tác vụ định kỳ mà hệ thống sẽ thực hiện.

**Câu lệnh cài đặt Cron:**

  * Cài đặt Cron

    ``# apt install cron``

    ![](/img/install_cron.png)

  * Kiểm tra trạng thái của Cron đã được cài đặt

    ``# systemctl status cron``

    ![](/img/checkcron.png)

**Câu lệnh Cron**

  * Tạo hoặc sửa file crontab

    ``# crontab -e``

  * Hiển thị file crontab
    
    ``# crontab -l``

  * Xoá file crontab
    
    ``# crontab -r``


Sau khi dùng lệnh crontab -e, ta sẽ thêm các task công việc chạy tự động

**Cấu trúc của 1 crontab**

    *     *     *     *     *     command to be executed
    -     -     -     -     -
    |     |     |     |     |
    |     |     |     |     +----- Ngàu trong tuần (0 - 6) (Chủ nhật=0)
    |     |     |     +------- Tháng (1 - 12)
    |     |     +--------- Ngày trong tháng (1 - 31)
    |     +----------- Giờ (0 - 23)
    +------------- Phút (0 - 59)

**Thực hành**

* Hiển thị các file thực hành

    ``# crontab -l``

    ![](/img/corntab-l.png)

* Mở crontab để chỉnh sửa

    Khi bạn mở crontab nếu là lần đầu thì nó sẽ hiện một bảng lựa chọn trình soạn thảo

    ![](/img/crontab-e-list.png)

* Thêm lệnh vào crontab

    In ra dòng chữ Hell world vào 6 giờ sáng mỗi ngày

    ``0 6 * * * echo "Hello world"``

Đó là hết phần tìm hiểu về crontab

## II. Khôi phục dữ liệu

Mất dữ liệu là điều mà tất cả người dùng PC tại một thời điểm nào đó phải đối mặt. Dù là sự cố ổ cứng hay do vô tình xóa, tất cả chúng ta đều đã từng ở trong những tình huống mà ước gì mình có thể lấy lại dữ liệu đã xóa.

**Ví dụ:**

Trong dường dẫn `/home` của mình có ``file1`` ``file2`` ``file3``

![](/img/home_file123.png)


Trước khi mình xoá hết tất cả các file thì mình sẽ sao lưu cả 3 file lại bằng lệnh ``tar``

``# tar -cf backup file1 file2 file3``

![](/img/tar_backup.png)

Muốn kiểm tra file backup có đủ 3 file không thì ta sẽ đùng lệnh

``# tar -tf backup``

![](/img/tar_tf.png)

Sau khi mình xoá cả 3 file thì mình sẽ giải nén file backup mình vừa nén trước đó. Ta dùng câu lệnh:

``# tar -xf backup``

![](/img/tar_xf.png)

Đó là cách khôi phục dữ liệu từ bản sao lưu cơ bản nhất

# END



