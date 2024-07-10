# Quản lí ổ đĩa và phân vùng

# Mục lục

## 1. Khái niệm về phân vùng và hệ thống tập tin

* **Phân vùng:** là quá trình chia ổ đĩa lưu trữ thành các phần nhỏ hơn, gọi là phân vùng, để sử dụng hiệu quả không gian lưu trữ và quản lý dữ liệu trên hệ thống máy tính.
    
    1. **Mục đích của phân vùng:** Phân vùng giúp tổ chức và quản lý dữ liệu trên ổ đĩa. Nó cho phép người dùng chia không gian lưu trữ thành các phần riêng biệt để cài đặt hệ điều hành, lưu trữ dữ liệu người dùng, và cài đặt các ứng dụng.

    2. **Loại phân vùng:**
       * **Primary Partition (Phân vùng chính):** Đây là các phân vùng cơ bản trên ổ đĩa. Mỗi ổ đĩa có thể có tối đa 4 primary partition. Primary partition có thể chứa hệ điều hành hoặc dữ liệu. 
       
       * **Extended Partition (Phân vùng mở rộng):** Extended partition không chứa dữ liệu trực tiếp mà nó là một loại container để chứa các logical partition bên trong. Mỗi ổ đĩa chỉ có thể có một extended partition.
       
       * **Logical Partition (Phân vùng logic):** Logical partition là các phân vùng bên trong extended partition. Nó cho phép vượt qua giới hạn 4 primary partition bằng cách tạo ra một không gian linh hoạt hơn để tổ chức dữ liệu.

    3. **Định dạng phân vùng:** Mỗi phân vùng sẽ có một định dạng hệ thống tập tin nhất định, chẳng hạn như NTFS trên Windows hoặc ext4 trên Linux. Định dạng này xác định cách dữ liệu được tổ chức và lưu trữ trên phân vùng.
    
    4. **Quản lý đa hệ điều hành (Multi-boot systems):** Phân vùng cũng cho phép cài đặt và quản lý nhiều hệ điều hành khác nhau trên cùng một máy tính. Mỗi hệ điều hành có thể được cài đặt trên một primary partition hoặc một logical partition.

    5. **Quản lý không gian lưu trữ:** Phân vùng giúp tối ưu hóa sử dụng không gian lưu trữ trên ổ đĩa, giúp dễ dàng sao lưu và khôi phục dữ liệu, cũng như cải thiện hiệu suất hệ thống.

    Tóm lại, cơ bản về phân vùng là một phần quan trọng trong quản lý hệ thống máy tính và lưu trữ dữ liệu, cung cấp cho người dùng các công cụ cần thiết để tổ chức, bảo vệ và quản lý dữ liệu hiệu quả trên các thiết bị lưu trữ.

* **Các hệ thống tập tin**
    * **Hệ thống tập tin Ext4, viết tắt của "fourth extended filesystem"**, đánh dấu bước tiến lớn trong công nghệ hệ thống tập tin trong thế giới Linux. Được phát triển như một sự cải tiến so với Ext3, Ext4 đã trở thành một trong những hệ thống tập tin phổ biến nhất trong hệ sinh thái Linux.

       1. **Journaling (Ghi nhật ký):** Ext4 sử dụng ghi nhật ký để đảm bảo tính nhất quán dữ liệu, làm cho nó trở thành một lựa chọn đáng tin cậy cho các ứng dụng quan trọng.
       
       2. **Extent-Based Storage (Lưu trữ dựa trên extent):** Ext4 sử dụng lưu trữ dựa trên extent, tối ưu hóa phân bổ file và cải thiện hiệu suất tổng thể.
       
       3. **Hiệu suất cải thiện:** Ext4 có hiệu suất đọc và ghi tốt hơn so với các phiên bản tiền nhiệm, phù hợp với nhiều khối công việc khác nhau.
       
        **Các Trường Hợp Sử Dụng của Ext4**
       
            Ext4 thích hợp cho các trường hợp sử dụng truyền thống như máy tính để bàn, laptop và máy chủ. Độ ổn định và tính tương thích của nó làm cho Ext4 trở thành lựa chọn mặc định cho nhiều bản phân phối Linux.
        
        **Giới Hạn của Ext4**
       
            Mặc dù có nhiều lợi ích, Ext4 vẫn có những giới hạn khi đến với khả năng mở rộng và các tính năng tiên tiến trong quản lý dữ liệu. Trong các tình huống yêu cầu khả năng mở rộng mạnh mẽ hoặc các tính năng quản lý dữ liệu tiên tiến, các hệ thống tập tin khác có thể phù hợp hơn.
    
        Tóm lại, Ext4 là một hệ thống tập tin mạnh mẽ và ổn định trong cộng đồng Linux, cung cấp sự đáng tin cậy cho nhiều ứng dụng từ các máy tính cá nhân đến các môi trường máy chủ quan trọng. Tuy nhiên, việc lựa chọn hệ thống tập tin nên phụ thuộc vào yêu cầu cụ thể của từng hệ thống và các tính năng kỹ thuật mong muốn.

    * **Hệ thống tập tin XFS:** một hệ thống tập tin hiệu suất cao có nguồn gốc từ thế giới Silicon Graphics (SGI), đã trở nên phổ biến nhờ tính mở rộng và độ bền của nó. Nó cung cấp những lợi thế đặc biệt cho các môi trường yêu cầu nhu cầu lưu trữ khó tính.

        1. **Khả năng mở rộng:** XFS vượt trội trong các kịch bản lưu trữ quy mô lớn, làm cho nó lý tưởng cho các giải pháp lưu trữ cấp doanh nghiệp.

        2. **Hiệu suất nâng cao cho các tệp lớn:** XFS được tối ưu hóa để xử lý các tệp lớn và khối lượng công việc lớn, làm cho nó trở thành lựa chọn hàng đầu cho các ứng dụng đa phương tiện và yêu cầu dữ liệu cao.

        3. **Xử lý siêu dữ liệu hiệu quả:** XFS quản lý siêu dữ liệu một cách hiệu quả, giảm thiểu các chướng ngại về hiệu suất và cải thiện tổng thể hiệu suất.

        **Các Trường Hợp Sử Dụng của XFS**
                
            XFS phù hợp trong các môi trường yêu cầu khả năng lưu trữ khổng lồ và tốc độ lớn, chẳng hạn như trung tâm dữ liệu, sản xuất phương tiện và tính toán khoa học.
        
        **Nhược điểm và Thách thức với XFS**

            Mặc dù XFS cung cấp khả năng mở rộng và hiệu suất vượt trội, nó có thể không phải là lựa chọn tốt nhất đối với các hệ thống quy mô nhỏ hoặc yêu cầu các tính năng tiên tiến như snapshotting và tính toàn vẹn tích hợp sẵn.
        
        Tóm lại, XFS là một hệ thống tập tin mạnh mẽ và linh hoạt, phù hợp cho các môi trường có nhu cầu lưu trữ lớn và yêu cầu hiệu suất cao. Tuy nhiên, việc lựa chọn hệ thống tập tin nên dựa trên yêu cầu cụ thể của từng ứng dụng và môi trường sử dụng.

    * **Hệ thống tập tin Btrfs viết tắt của "B-tree filesystem"**, đại diện cho sự phát triển tiên tiến nhất trong lĩnh vực hệ thống tập tin Linux. Nó ra đời với mong muốn giải quyết những hạn chế của các hệ thống tập tin hiện có và mang đến những tính năng đổi mới có thể thay đổi cách chúng ta quản lý dữ liệu.
        1. **Chức năng Copy-on-Write (CoW):** Btrfs sử dụng CoW để đảm bảo tính toàn vẹn dữ liệu và cho phép tạo snapshot hiệu quả, làm cho nó trở thành một công cụ mạnh mẽ cho quản lý dữ liệu.
        
        2. **Dữ liệu dự phòng tích hợp và Snapshot:** Btrfs bao gồm các tính năng như chức năng tương tự RAID và snapshots, đơn giản hóa việc bảo vệ và khôi phục dữ liệu.
        
        3. **Sửa chữa và Bảo trì Hệ thống tập tin trực tuyến:** Btrfs cho phép thực hiện các hoạt động sửa chữa và bảo trì hệ thống tập tin trực tuyến, giảm thiểu thời gian ngừng hoạt động.
        
        **Các Trường Hợp Sử Dụng của Btrfs**

            Btrfs rất phù hợp cho các kịch bản yêu cầu quản lý dữ liệu tiên tiến, như ảo hóa, containerization và các kịch bản yêu cầu tính toàn vẹn dữ liệu và linh hoạt cao.
        
        **Các Yếu tố Cần Xem Xét và Vấn Đề Tiềm Ẩn của Btrfs**

            Mặc dù Btrfs cung cấp nhiều tính năng tiên tiến, nó có thể không phải lựa chọn lý tưởng cho mọi trường hợp sử dụng. Người dùng nên cẩn thận đánh giá các khả năng của nó và xem xét các yếu tố như tính ổn định và hỗ trợ từ cộng đồng.
    
        Tóm lại, Btrfs là một hệ thống tập tin tiên tiến và mạnh mẽ trong cộng đồng Linux, mang đến những tính năng và lợi ích đáng chú ý cho quản lý và bảo vệ dữ liệu. Tuy nhiên, sự lựa chọn hệ thống tập tin phù hợp nên dựa trên yêu cầu cụ thể của từng ứng dụng và các yếu tố kỹ thuật khác.

## 2. Tạo, xóa và quản lý phân vùng

### 1. Hiểu về MBR và GPT

* **MBR (Master Boot Record)**
    MBR là một hệ thống phân vùng được sử dụng từ những ngày đầu của MS-DOS (cụ thể là PC-DOS 2.0 từ năm 1983) và trong nhiều thập kỷ là chuẩn phân vùng trên các máy tính cá nhân. Bảng phân vùng được lưu trữ trên sector đầu tiên của đĩa, được gọi là Boot Sector, cùng với một boot loader, trên các hệ thống Linux thường là GRUB bootloader. Tuy nhiên, MBR có những hạn chế nhất định như không thể xử lý các đĩa có kích thước lớn hơn 2 TB và giới hạn chỉ 4 phân vùng chính trên mỗi đĩa.

* **GPT (GUID Partition Table)**
    GPT là một hệ thống phân vùng giải quyết nhiều hạn chế của MBR. Không có giới hạn thực tế về kích thước đĩa và số lượng phân vùng tối đa chỉ phụ thuộc vào hệ điều hành. GPT thường được sử dụng phổ biến trên các máy tính hiện đại sử dụng UEFI thay vì BIOS truyền thống.

* **Quản lý hệ thống**
    Trong các tác vụ quản trị hệ thống, rất có thể bạn sẽ gặp cả hai chuẩn này, vì vậy quan trọng để biết cách sử dụng các công cụ liên quan để tạo, xóa hoặc chỉnh sửa các phân vùng:

    1. **MBR:** Sử dụng các công cụ như ``fdisk``, ``parted`` để quản lý phân vùng trên các đĩa sử dụng MBR.
    
    2. **GPT:** Để quản lý phân vùng trên các đĩa sử dụng GPT, bạn có thể sử dụng ``gdisk``, ``parted``, ``GParted``, hoặc các công cụ quản lý phân vùng tích hợp trong hệ điều hành như ``diskpart`` trên Windows.

### 2. Sử dụng Fdisk để quản lí MBR
* **Công cụ tiêu chuẩn để quản lý các phân vùng MBR trên Linux là ``fdisk``**. Đây là một công cụ tương tác, dựa trên menu. Để sử dụng, bạn gõ lệnh fdisk sau đó là tên thiết bị tương ứng với đĩa mà bạn muốn chỉnh sửa. Ví dụ, câu lệnh thực hiện là:
        
        # fdisk /dev/sda

    Khi được gọi, fdisk sẽ hiển thị một lời chào và sau đó là một cảnh báo, sau đó nó sẽ chờ lệnh từ bạn để thực hiện các thao tác trên đĩa.

    ![Image description](/thuctap/img/fdisk.png)

    Cảnh báo này rất quan trọng. Bạn có thể tạo, chỉnh sửa hoặc xóa các phân vùng một cách tự do, nhưng không có gì sẽ được ghi vào đĩa trừ khi bạn sử dụng lệnh ghi ``(w)``. Vì vậy, bạn có thể "thực hành" mà không lo lắng mất dữ liệu, miễn là bạn không nhấn phím ``w``. Để thoát khỏi fdisk mà không lưu các thay đổi, bạn sử dụng lệnh ``q``.

    **Xem bảng phân vùng hiện tại**
    Lệnh ``p`` trong fdisk được sử dụng để in bảng phân vùng hiện tại. Đầu ra thường có dạng như sau:

    ![Image description](/thuctap/img/fdisk_p.png)

    **Đây là mô tả ý nghĩa của từng cột trong bảng phân vùng**

    ``Device``: Thiết bị được gán cho phân vùng

    ``Start``: Số sector bắt đầu của phân vùng.

    ``End``: Số sector kết thúc của phân vùng.

    ``Sectors``: Tổng số sector trong phân vùng. Nhân với kích thước sector để lấy kích thước phân vùng tính bằng byte.

    ``Size``: Kích thước của phân vùng ở dạng "human readable" (ví dụ: đơn vị là gigabyte).

    ``Type``: Mô tả loại phân vùng.

    **Phân vùng Primary và Extended**

    Trên ổ đĩa MBR, bạn có thể có 2 loại phân vùng chính: phân vùng chính (primary) và phân vùng mở rộng (extended). Như đã đề cập trước đó, bạn chỉ có thể có tối đa 4 phân vùng chính trên đĩa, và nếu bạn muốn đĩa cứng có thể "bootable", phân vùng đầu tiên phải là phân vùng chính.

    Một cách để vượt qua giới hạn này là tạo một phân vùng mở rộng (extended), nó sẽ làm nhiệm vụ như một bao chứa cho các phân vùng logic. Ví dụ, bạn có thể có một phân vùng chính, một phân vùng mở rộng chiếm toàn bộ không gian còn lại của đĩa và năm phân vùng logic bên trong nó.

    Đối với hệ điều hành như Linux, phân vùng chính và phân vùng mở rộng được xử lý hoàn toàn giống nhau, vì vậy không có "ưu điểm" nào khi sử dụng một loại hơn loại khác.

    **Tạo một phân vùng**

    Để tạo một phân vùng, bạn sử dụng lệnh ``n``. Theo mặc định, các phân vùng sẽ được tạo ở đầu của không gian chưa phân vùng trên ổ cứng. Bạn sẽ được yêu cầu chọn loại phân vùng (primary hoặc extended), ``Start Sector`` và ``End Sector``.

    Đối với ``Start Sector``, bạn thường có thể chấp nhận giá trị mặc định được đề xuất bởi ``fdisk``, trừ khi bạn cần phân vùng bắt đầu từ một sector cụ thể. Thay vì chỉ định ``End Sector``, bạn có thể chỉ định kích thước theo đơn vị K, M, G, T hoặc P (Kilo, Mega, Giga, Tera hoặc Peta).
    
    Ví dụ, nếu bạn muốn tạo một phân vùng 1 GB, bạn có thể chỉ định +1G làm ``End Sector``, và ``fdisk`` sẽ cấp phát kích thước phân vùng tương ứng. Xem ví dụ sau để tạo một phân vùng chính:

    ![Image description](/thuctap/img/fdisk_n.png)

    **Kiểm tra xem còn dung lượng trống không**
    
    Nếu bạn không biết có bao nhiêu không gian trống trên đĩa, bạn có thể sử dụng lệnh ``F`` để hiển thị không gian chưa phân vùng, như sau:

    ![Image description](/thuctap/img/fdisk_F.png)
