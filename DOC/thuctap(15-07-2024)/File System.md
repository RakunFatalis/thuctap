# FILE SYSTEM

# MỤC LỤC


- [FILE SYSTEM](#file-system)
- [MỤC LỤC](#mục-lục)
  - [1. Bố cục hệ thống tệp](#1-bố-cục-hệ-thống-tệp)
  - [2. Các loại hệ thống tập tin](#2-các-loại-hệ-thống-tập-tin)
  - [3. Thao tác với ổ cứng](#3-thao-tác-với-ổ-cứng)
    - [A. Làm việc với disk](#a-làm-việc-với-disk)
    - [B. Định dạng](#b-định-dạng)
    - [C. Mount File](#c-mount-file)
    - [D. File fstab](#d-file-fstab)
  - [4. Inode, symlink, hardlink](#4-inode-symlink-hardlink)
    - [A. Inode](#a-inode)
    - [B. Symlink](#b-symlink)
    - [C. Hardlink](#c-hardlink)
    - [D. Bảng so sánh giữa Symlink và Hardlink](#d-bảng-so-sánh-giữa-symlink-và-hardlink)
- [END](#end)

## 1. Bố cục hệ thống tệp

Bố cục hệ thống tệp (File System Layout) đề cập đến cách tổ chức và lưu trữ dữ liệu trên thiết bị lưu trữ (như ổ cứng) ở mức độ thấp hơn. Điều này bao gồm các cấu trúc dữ liệu vật lý và logic cần thiết để quản lý các tệp và thư mục.

Dưới đây là ảnh minh hoạ về bố cục hệ thống tệp:

![](/img/FileSystemLayout.png)

Đa số các bố cục hệ thống tệp đều sẽ có các thành phần chính sau:

* **Superblock:**

    Chứa thông tin quan trọng về file system, chẳng hạn như kích thước, kiểu file system, và thông tin về các khối dữ liệu (blocks). Superblock thường nằm ở đầu của file system.

* **Inodes**:

    Cấu trúc dữ liệu lưu trữ thông tin về các tệp và thư mục, bao gồm quyền truy cập, kích thước, và địa chỉ của các khối dữ liệu chứa nội dung của tệp. Mỗi tệp hoặc thư mục đều có một inode riêng.

* **Data Blocks**:

    Chứa nội dung thực tế của tệp. Khi tệp được lưu trữ trên ổ đĩa, dữ liệu của tệp được phân phối trong các khối dữ liệu.

* **Directory Entries**:

    Cấu trúc lưu trữ thông tin về tên tệp và liên kết đến inode tương ứng. Thư mục chứa các mục nhập (entries) mà mỗi mục nhập đại diện cho một tệp hoặc thư mục con, kèm theo inode của nó.

* **Free Space Management**:

    Quản lý không gian trống trong file system, giúp theo dõi các khối dữ liệu chưa được sử dụng để có thể phân phối chúng cho các tệp mới hoặc mở rộng các tệp hiện có.

* **Journal** (nếu có):

    Được sử dụng trong các file system hỗ trợ tính năng journaling (ghi nhật ký) để ghi lại các thay đổi sắp tới. Điều này giúp bảo vệ file system khỏi sự hỏng hóc dữ liệu do mất điện hoặc sự cố hệ thống.

## 2. Các loại hệ thống tập tin

Trên mỗi hệ điều hành đều sẽ có các loại file system khác nhau. Tại đây ta sẽ chỉ nói những file system phổ biến thường được dùng trên hệ điều hảnh Linux:

* **Ext2**:

    Ext2 được định nghĩa là hệ thống tập tin mở rộng thứ hai. Nó được giới thiệu vào năm 1993 và là hệ thống tập tin thương mại đầu tiên được thiết kế để khắc phục những hạn chế của hệ thống tập tin Ext. Ext2 không có tính năng journaling (ghi nhật ký), và nó được khuyến nghị cho các ổ đĩa flash và USB. Kích thước tệp cá nhân mà Ext2 hỗ trợ là 2TB và có thể từ 4TB đến 32TB tùy thuộc vào kích thước khối (block size).

    ![](/img/ext2.jpg)


* **Ext3**:

    Ext3 là hệ thống tập tin mở rộng thứ ba. Hệ thống tập tin journaling này được sử dụng trên nhiều bản phân phối Linux. Nó có khả năng theo dõi tất cả các thay đổi được thực hiện với Ext3 để cải thiện độ tin cậy và giảm thiểu khả năng hỏng hóc hệ thống tập tin. Ngoài ra, nó cho phép bạn nâng cấp từ Ext2 mà không cần sao lưu và khôi phục dữ liệu.

    ![](/img/ext3.jpg)

    Ext3 là sự cải tiến đáng kể so với Ext2, với tính năng journaling giúp tăng cường độ tin cậy và an toàn của hệ thống tập tin, đồng thời cho phép nâng cấp dễ dàng từ Ext2 mà không cần thao tác phức tạp với dữ liệu.

* **Ext4**:

    Ext4 là một chuỗi các mở rộng tương thích ngược với Ext2. Nó cũng là hệ thống tập tin cho hầu hết các bản phân phối Linux. Ext4 được hỗ trợ bởi các hệ điều hành khác, bao gồm Windows, FreeBSD, macOS, và KolibriOS (chỉ đọc).

    ![](/img/ext4.jpg)

    Ext4 được giới thiệu ban đầu để mở rộng giới hạn lưu trữ và cải thiện hiệu suất hệ thống. So với hệ thống Ext trước đó, Ext4 có thể hỗ trợ kích thước phân vùng lên đến 1EB và kích thước tệp đơn lên đến 16TB với kích thước khối chuẩn 4K.

* **XFS**:

    XFS là một hệ thống tập tin hiệu suất cao 64-bit với tính năng ghi nhật ký, được tạo ra bởi Silicon Graphics, Inc (SGI) vào năm 1993. Nó là hệ thống tập tin mặc định trong hệ điều hành IRIX của SGI kể từ phiên bản 5.3. XFS đã được port sang kernel Linux vào năm 2001; tính đến tháng 6 năm 2014, XFS được hầu hết các bản phân phối Linux hỗ trợ; Red Hat Enterprise Linux sử dụng XFS làm hệ thống tập tin mặc định của nó.

    **XFS thường được sử dụng cho:**

    * Các máy chủ lớn với tài nguyên dồi dào.
    * Các tình huống xử lý tệp lớn và hoạt động I/O cao.
    * Môi trường yêu cầu xử lý nhiều luồng đồng thời.

    **Điểm mạnh:**

    * Hiệu suất cao với các tệp lớn và các ứng dụng đa luồng.
    * Mở rộng tốt với kích thước lưu trữ và hệ thống tập tin tăng lên.
    * Xử lý hiệu quả các hoạt động I/O song song.
    
    XFS lý tưởng cho các môi trường tính toán hiệu suất cao, cơ sở dữ liệu lớn hoặc máy chủ tệp nơi khả năng xử lý khối lượng dữ liệu lớn và truy cập đồng thời là rất quan trọng.

* **Btrfs**
    
    Btrfs là một định dạng lưu trữ máy tính kết hợp giữa hệ thống tập tin dựa trên nguyên tắc sao chép khi ghi (copy-on-write, COW) với một trình quản lý khối lượng logic (không nên nhầm lẫn với LVM của Linux).

    Btrfs được thiết kế để giải quyết sự thiếu hụt về việc gộp nhóm, snapshot, kiểm tra tính toàn vẹn (checksums), và khả năng mở rộng đa thiết bị trong các hệ thống tập tin của Linux

    **Ưu Điểm**
    
    * **Khả năng mở rộng và linh hoạt**: Btrfs cung cấp các tính năng nâng cao cho việc quản lý và bảo trì hệ thống tập tin, với khả năng mở rộng và điều chỉnh linh hoạt.
    * **Bảo mật và tính toàn vẹn**: Các tính năng như snapshot, checksumming và self-healing giúp đảm bảo tính toàn vẹn và bảo mật dữ liệu.
    * **Quản lý RAID đơn giản**: Tích hợp hỗ trợ RAID giúp dễ dàng cấu hình và quản lý RAID mà không cần phần mềm RAID riêng biệt.

    **Nhược Điểm**

    * **Tính ổn định**: Mặc dù Btrfs đã phát triển mạnh mẽ, một số người dùng vẫn lo ngại về tính ổn định và sự trưởng thành của nó so với ext4 và XFS.
    * **Hiệu suất**: Trong một số trường hợp, Btrfs có thể có hiệu suất thấp hơn so với ext4 hoặc XFS, đặc biệt là khi xử lý các tác vụ I/O nặng.

    Btrfs thường được sử dụng trong các các máy chủ và môi trường lưu trữ yêu cầu tính năng snapshot, RAID tích hợp, và khả năng tự phục hồi, được sử dụng cho các máy tính cá nhân khi cần tính năng bảo vệ dữ liệu nâng cao và khả năng quản lý không gian lưu trữ linh hoạt.

* **JFS (Journaled File System)**

    JFS là một hệ thống tập tin được thiết kế để cung cấp tính toàn vẹn và hiệu suất cao. Nó được phát triển bởi IBM và được giới thiệu lần đầu vào năm 1990. JFS có một số phiên bản, với JFS2 là phiên bản nâng cấp được sử dụng phổ biến hơn.

    JFS là một lựa chọn tốt cho các hệ thống tập tin cần tính toàn vẹn và hiệu suất ổn định, nhưng có thể không phù hợp với tất cả các trường hợp sử dụng, đặc biệt khi so sánh với các hệ thống tập tin hiện đại như XFS hoặc Btrfs.

## 3. Thao tác với ổ cứng

### A. Làm việc với disk
 
* **Hiển thị thông tin đisk**

Có nhiều cách để hiển thị thông tin ổ đĩa của máy bạn, tại đây ta sẽ dùng những cách thường dùng trên linux

Ta sử dụng câu lệnh **lsblk** để hiện tổng quát các ổ đĩa và phần vùng của chúng

![](/img/listdisk.png)


Hiển thị thông tin chi tiết của về các phân vùng và bảng phân vùng của chúng ta sử dụng câu lệnh ``fdisk -l``

Cung cấp thông tin về phân vùng và bảng phân vùng của các disk mà dùng dạng GPT và MBR, ta sẽ dụng ``parted -l``


### B. Định dạng

Trong linux ta có thể sử dụng lệnh **mkfs** để format một phân vùng hoặc một ổ đĩa

Cú pháp cơ bản của câu lệnh: ``# mkfs.<filesystem> </path/to/disk/partition>``


Dưới đây là các bước để chúng ta định dạng một ổ đĩa hoặc một phân vùng

* **Bước 1: Xác định các ổ đĩa hoặc một phân vùng**

    Ta dùng lệnh `lsblk` để liệt kê ra
    
    ![](/img/lsblk_f.png)


* **Bước 2: Format thiết bị**

    Giả sử mình muốn format ``/dev/sdb2`` thành hệ thống file ext4, ta sử dụng câu lệnh ``mkfs`` đã nêu ở trên

    ``# mkfs.ext4 /dev/sdb2``

    ![](/img/mkfs_Ext4.png)

>[!WARNING]
>Vsiệc format sẽ xóa sạch dữ liệu trên thiết bị đó, vì vậy hãy đảm bảo sao lưu dữ liệu quan trọng trước khi tiến hành.

### C. Mount File

  * **Hiển thị thông tin về các file system được mount:**

    ![Image description](/img/mount_ext4.png)

  * **Mount các file system:**

    ![Image description](/img/mount_file.png)

  * **Hiển thị thông tin phiên bản:**

    ![Image description](/img/mount_ver.png)

  * **Umount filesystem:**
    
    ![Image description](/img/umount_.png)

### D. File fstab

* **Fstab là gì?**

Fstab hay còn gọi là ``File System Table`` là một tệp cấu hình quan trọng trong hệ điều hành Linux. Nó chứa thông tin về các hệ thống tập tin và thiết bị lưu trữ cần được mount tự động khi hệ thống khởi động. Fstab giúp quản lý và kiểm soát các hệ thống tập tin và thiết bị lưu trữ được gắn vào hệ thống Linux, đảm bảo tính ổn định và hiệu suất của hệ thống.

Tệp Fstab nằm ở trong thư mục “etc”.  Đường dẫn cụ thể là “``/etc/fstab``”. Dưới đây là một mẫu nội dung mặc định của file fstab

![](/img/file_fstab.png)


* **Cấu trúc chung của file fstab**

Như bạn có thể thấy ở trong hình, cấu trúc của 1 fstab bao gồm

``<file system>  <mount point>  <type>  <options>  <dump>  <pass>``

**Trong đó:**

``<file system>``: Hệ thống file hoặc thiết bị. Đây có thể là đường dẫn đến thiết bị (ví dụ: /dev/sda1), UUID (ví dụ: UUID=xxxx-xxxx), hoặc nhãn (label) (ví dụ: LABEL=mydisk).

``<mount point>``: Thư mục nơi hệ thống file sẽ được gắn kết (mount). Ví dụ: /, /home, /mnt/data.

``<type>``: Loại hệ thống file (ví dụ: ext4, xfs, btrfs, vfat, ntfs).

``<options``>: Các tùy chọn gắn kết. Một số tùy chọn phổ biến bao gồm defaults, ro (chỉ đọc), rw (đọc-ghi), noatime, nodiratime, nosuid, noexec, user, và auto.

``<dump>``: Tần suất sao lưu hệ thống file bằng lệnh dump. Thường được đặt là 0 nếu không sử dụng dump.

``<pass``>: Thứ tự kiểm tra hệ thống file bằng lệnh fsck khi khởi động. 1 cho hệ thống file gốc (/), 2 cho các hệ thống file khác, và 0 để bỏ qua kiểm tra.

* **Các tuỳ chọn của file fstab**

| Tùy chọn   | Mô tả                                                                                   |
|------------|-----------------------------------------------------------------------------------------|
| ``defaults``   | Bao gồm các tùy chọn `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, và `async`.         |
| ``ro``         | Gắn kết hệ thống file ở chế độ chỉ đọc.                                                 |
| ``rw``         | Gắn kết hệ thống file ở chế độ đọc-ghi.                                                 |
| ``noatime``    | Không cập nhật thời gian truy cập.                                                      |
| ``nodiratime`` | Không cập nhật thời gian truy cập cho thư mục.                                          |
| ``noexec``     | Không cho phép thực thi các tệp tin nhị phân.                                           |
| ``nosuid``     | Không cho phép các tệp tin `set-user-ID` hoặc `set-group-ID` chạy với quyền root.       |
| ``user``       | Cho phép người dùng không phải root gắn kết và tháo gỡ hệ thống file.                  |
| ``async``      | Thực hiện các thao tác nhập/xuất không đồng bộ (asynchronous I/O).                      |

* **Thay đổi địa chỉ gắn kết mà không cần phải tháo gỡ với lệnh remount**

Cú pháp cơ bản của lệnh remount : ``# mount -o remount,<new_options> <mount_point>``

**Trong đó:**

``<new_options>`` là các tùy chọn mới mà bạn muốn áp dụng.

``<mount_point>`` là thư mục gắn kết hiện tại của hệ thống file.

Ví dụ sử dụng

**Chuyển từ chế độ chỉ đọc sang chế độ đọc-ghi**

Nếu một hệ thống file đã được gắn kết ở chế độ chỉ đọc (read-only) và bạn muốn chuyển sang chế độ đọc-ghi (read-write), bạn có thể sử dụng lệnh sau:

``# mount -o remount,rw /mnt/mydisk``

## 4. Inode, symlink, hardlink

### A. Inode

Inode (Index Node) là một cấu trúc dữ liệu trong hệ thống tệp của Unix/Linux dùng để lưu trữ thông tin về một tệp hoặc thư mục. Mỗi tệp hoặc thư mục trên hệ thống tệp đều có một inode tương ứng. Inodes nắm vai trò như một mã định danh duy nhất dành cho một loại siêu dữ liệu trên các hệ thống tệp nhất định.

**Cách kiểm tra inode**

Ta sử dụng lệnh ``df -i`` để kiểm tra số lượng hiện đang có trong hệ thống

![](/img/inode_df.png)



* **Cấu trúc của inode**

    **inode number**: Mỗi inode có một số định danh duy nhất trong hệ thống tệp, gọi là số inode. Đây là cách hệ thống tệp nhận diện inode cụ thể.

    **Metadata:** inode lưu trữ thông tin metadata về tệp hoặc thư mục, bao gồm:
    * Kích thước tệp.
    * Quyền truy cập (quyền đọc, ghi, thực thi).
    * Thời gian tạo (ctime), thời gian sửa đổi (mtime), và thời gian truy cập (atime).
    * Số liên kết cứng (hard link count).
    * ID người dùng (UID) và ID nhóm (GID) của chủ sở hữu tệp.

    **Địa chỉ**: inode chứa con trỏ đến các khối dữ liệu thực sự trên đĩa nơi nội dung của tệp được lưu trữ.

### B. Symlink

Symlink (Symbolic Link) là loại liên kết mềm và có thể trỏ đến bất kỳ tập tin hoặc thư mục nào, kể cả các đường dẫn tương đối hoặc tuyệt đối. Symlink lưu trữ đường dẫn của mục tiêu và có thể dễ dàng được tạo ra và xóa bỏ. Nếu mục tiêu của symlink bị xóa hoặc di chuyển, symlink sẽ trở thành "hỏng" và không còn trỏ đến mục tiêu đúng.

Có thể hiểu Symbolic Link đơn giản là đường dẫn trỏ đến vị trí của file nào đó trong hệ thống máy tính. Bạn có thể tạo nhiều symbolic links đặt ở nhiều nơi khác nhau nhưng vẫn trỏ về đúng 1 file gốc. Vì vậy, gia tăng tính tiện lợi cho việc tìm kiếm file trong một dòng lệnh.


**Tạo symlink trong linux**

Để tạo một symlink, bạn sử dụng lệnh ``ln`` với tùy chọn ``-s``. Cú pháp của lệnh như sau:

``# ln -s /path/to/original /path/to/symlink``

>[!WARNING]
>**Lưu Ý**
>* **Symlink có thể trỏ đến đường dẫn tuyệt đối hoặc tương đối**. Đường dẫn tuyệt đối bắt đầu từ gốc hệ thống (/), còn đường dẫn tương đối bắt đầu từ thư mục hiện tại.
>
>* **Nếu mục tiêu của symlink bị xóa hoặc di chuyển, symlink sẽ trở thành "hỏng" hoặc "dangling"**. Symlink không tự động cập nhật đường dẫn đến mục tiêu mới.
>
>* **Symlink không thay đổi quyền của tập tin gốc**. Quyền truy cập vào symlink thường được quản lý bởi quyền của tập tin gốc.

### C. Hardlink

Hardlink là một loại liên kết đến một tập tin trên hệ thống tệp. Khi bạn tạo một hardlink, bạn thực chất tạo một mục nhập mới trong hệ thống tệp, nhưng mục nhập này trỏ đến cùng một inode (đơn vị lưu trữ dữ liệu của tập tin) như tập tin gốc.

**Tạo Hardlink trong linux**

Để tạo một hardlink, bạn có thể sử dụng lệnh ``ln`` trong Linux. Ví dụ:

``# ln /path/to/originalfile /path/to/hardlink``

**Trong đó**:

  * ``/path/to/originalfile`` là đường dẫn đến tập tin gốc.

  * ``/path/to/hardlink`` là đường dẫn đến hardlink mới.

>[!WARNING]
>**Lưu ý**:
>* Hardlink không thể liên kết đến thư mục (trừ thư mục gốc) vì điều này có thể gây ra vấn đề về vòng lặp trong hệ thống tệp.
>* Hardlink không thể liên kết giữa các hệ thống tệp khác nhau. Tất cả các liên kết cứng phải nằm trong cùng một hệ thống tệp.

### D. Bảng so sánh giữa Symlink và Hardlink

| **Tiêu Chí** | **Hardlink**| **Symlink**|
|--------------|---------|------------|
| **Cấu Trúc**| Tạo một mục nhập mới trỏ đến cùng một inode | Tạo một tập tin chứa đường dẫn đến tập tin/thư mục gốc |
| **Dữ Liệu**| Không sao chép dữ liệu; cùng một inode| Là tập tin chứa đường dẫn đến tập tin/thư mục gốc |
| **Tính Toán**| Có cùng quyền truy cập và sửa đổi dữ liệu| Nếu tập tin gốc bị xóa, symlink trở thành liên kết bị hỏng |
| **Xóa**| Tập tin không bị xóa cho đến khi tất cả hardlink bị xóa| Symlink có thể bị xóa độc lập; không bị ảnh hưởng nếu tập tin gốc bị xóa |
| **Thư Mục**| Không thể liên kết đến thư mục (trừ thư mục gốc)| Có thể liên kết đến cả tập tin và thư mục |
| **Thay Đổi Tập Tin**| Thay đổi ở một hardlink sẽ ảnh hưởng đến tất cả các hardlink | Thay đổi tập tin gốc sẽ ảnh hưởng đến tất cả các symlink |
| **Hỗ Trợ**| Giới hạn trong cùng một hệ thống tệp| Có thể liên kết giữa các hệ thống tệp khác nhau |
| **Kiểm Tra Inode**| Các hardlink đến cùng một inode có cùng số inode | Symlink có số inode riêng biệt và chứa đường dẫn |



# END

