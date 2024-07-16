# BOOT PROCESS

# Mục lục





## Power Supply Unit

Quá trình khởi động của máy tính bắt đầu khi bạn nhấn nút nguồn, tạo ra một mạch điện kín làm cho bộ nguồn (PSU) thực hiện tự kiểm tra. Để quá trình khởi động tiếp tục, tự kiểm tra này phải hoàn thành thành công. Nếu bộ nguồn không thể xác nhận tự kiểm tra, thường sẽ không có đầu ra nào cả.

Các máy tính x86 hiện đại, đặc biệt là những máy sử dụng chuẩn ATX, sẽ có hai đầu nối chính tới bo mạch chủ: một đầu nối 4 chân để cấp nguồn cho CPU và một đầu nối 24 chân để cấp nguồn cho các thành phần khác của bo mạch chủ. Nếu tự kiểm tra thành công, PSU sẽ gửi tín hiệu đến CPU qua đầu nối 4 chân để chỉ ra rằng nó nên khởi động.

**Lỗi có thể xảy ra:**

PSU không thể thực hiện tự kiểm tra thành công: Điều này có thể do PSU bị hỏng, ví dụ như cầu chì bị cháy hoặc các hư hỏng khác do quá dòng hoặc quá áp trên đường dây điện.

**Cách khắc phục:**

Sử dụng bộ lưu điện hoặc bộ chống sét tốt: Để bảo vệ hệ thống khỏi các sự cố điện như vậy, việc sử dụng một bộ lưu điện (UPS) hoặc một bộ chống sét (SPD) tốt luôn được khuyến nghị.

**Quá trình chi tiết:**
* 1. Nhấn nút nguồn: Khi nút nguồn được nhấn, mạch điện được hoàn thành, cho phép dòng điện chạy qua PSU.

* 1. Tự kiểm tra PSU: PSU sẽ thực hiện một loạt kiểm tra tự động để đảm bảo rằng nó hoạt động bình thường và có thể cung cấp điện cho các thành phần khác của hệ thống.

  * Kiểm tra điện áp: PSU kiểm tra các mức điện áp đầu ra để đảm bảo chúng nằm trong phạm vi an toàn.

  * Kiểm tra quá tải: PSU kiểm tra các điều kiện quá tải để đảm bảo không có thành phần nào tiêu thụ quá nhiều điện.

* 3. Gửi tín hiệu bật: Nếu tự kiểm tra thành công, PSU sẽ gửi một tín hiệu tới CPU thông qua đầu nối 4 chân để cho phép CPU bắt đầu khởi động.

* 4. Khởi động CPU và bo mạch chủ: CPU bắt đầu thực hiện các quy trình khởi động, bao gồm kiểm tra bộ nhớ, tải BIOS/UEFI và khởi chạy hệ điều hành.

Việc đảm bảo rằng PSU và các thành phần khác của hệ thống hoạt động đúng cách là rất quan trọng để đảm bảo quá trình khởi động diễn ra suôn sẻ.



## BIOS and CMOS

### 1. BIOS (Basic Input/Output System)

BIOS là một mạch tích hợp (IC) nằm trên bo mạch chủ của máy tính, có thể được lập trình với phần mềm cố định (firmware). Phần mềm cố định này hỗ trợ quá trình khởi động để hệ điều hành có thể tải.

**Chi tiết:**

1. **Firmware**: Phần mềm cố định được lập trình vào bộ nhớ EEPROM (Electrically Erasable Programmable Read-Only Memory). Trong trường hợp này, firmware hỗ trợ quá trình khởi động hệ điều hành và cấu hình các cài đặt phần cứng cơ bản.

2. **IC (Integrated Circuit)**: Là một vi mạch điện tử, thường được coi là một "chip máy tính" - một tấm wafer mỏng được đóng gói và có các dấu vết kim loại nhô ra có thể gắn lên bo mạch in.

BIOS là giao diện cấp thấp nhất mà bạn có thể tiếp cận với phần cứng trong máy tính. BIOS cũng thực hiện kiểm tra tự động khi bật nguồn (Power-On Self Test, hay POST).

**Quá trình BIOS:**

1. **Khởi động CPU**: Khi CPU được cấp nguồn, cuộc gọi đầu tiên được thực hiện là tới BIOS.

2. **POST**: BIOS thực hiện kiểm tra tự động để đảm bảo rằng các phần cứng tối thiểu cần thiết tồn tại:

    * CPU

    * Bộ nhớ

    * Card đồ họa

3. **Cấu hình phần cứng**: Sau khi xác nhận sự tồn tại của phần cứng, chúng phải được cấu hình.

### 2. CMOS (Complementary Metal Oxide Semiconductor)

CMOS là bộ nhớ lưu trữ của BIOS, chứa tất cả các cài đặt mà BIOS cần lưu trữ, chẳng hạn như tốc độ bộ nhớ, hệ số nhân của CPU, và vị trí cùng cấu hình của các ổ cứng và thiết bị khác.

**Quá trình cấu hình BIOS:**

1. **Thiết lập tần số bộ nhớ**: BIOS lấy tần số bộ nhớ và cố gắng thiết lập nó trên bộ điều khiển bộ nhớ.

2. **Thiết lập tốc độ CPU**: BIOS nhân tần số bộ nhớ với hệ số nhân của CPU để xác định tốc độ chạy của CPU.
   
   * Đôi khi có thể "ép xung" (overclock) CPU bằng cách đặt nó chạy ở hệ số nhân cao hơn thiết kế ban đầu, làm cho CPU chạy nhanh hơn. Việc này có thể mang lại lợi ích nhưng cũng có rủi ro, bao gồm khả năng làm hỏng CPU.

## POST test

Quá trình Power-On Self Test (POST) là một phần quan trọng của quá trình khởi động máy tính, được thực hiện bởi BIOS sau khi các tần số của bộ nhớ và CPU đã được thiết lập. POST thực hiện các kiểm tra cơ bản trên nhiều thành phần hệ thống để đảm bảo chúng hoạt động đúng.

Các kiểm tra của POST:

1. **Kiểm tra bộ nhớ**: Đảm bảo rằng bộ nhớ đang hoạt động tốt.

2. **Kiểm tra ổ cứng và các thiết bị khác**: Xác nhận rằng các ổ cứng và thiết bị khác đang phản hồi.

3. **Kiểm tra bàn phím và chuột**: Đảm bảo rằng bàn phím và chuột đã được kết nối (kiểm tra này thường có thể bị vô hiệu hóa).

4. **Khởi tạo các BIOS bổ sung**: Khởi tạo bất kỳ BIOS bổ sung nào có thể được cài đặt (ví dụ: card RAID).

**Các lỗi có thể xảy ra:**

Khi một kiểm tra POST thất bại, BIOS sẽ thường báo hiệu lỗi thông qua một loạt tiếng bíp trên loa nội bộ của máy tính. Mẫu tiếng bíp chỉ ra kiểm tra cụ thể nào đã thất bại. Một số mã bíp phổ biến trên các hệ thống:

**1. Một tiếng bíp**: Tất cả các kiểm tra đã vượt qua thành công.

**2. Ba tiếng bíp**: Thường là lỗi bộ nhớ.

**3. Một tiếng bíp dài, hai tiếng bíp ngắn**: Lỗi card đồ họa hoặc vấn đề hiển thị.

**Chi tiết quá trình:**

**1. Thiết lập tần số bộ nhớ và CPU**: BIOS lấy tần số bộ nhớ và hệ số nhân của CPU để thiết lập tốc độ chạy của CPU.

**2. Khởi động POST**: BIOS bắt đầu thực hiện các kiểm tra POST trên các thành phần hệ thống.

**3. Kiểm tra bộ nhớ**: POST kiểm tra xem bộ nhớ có hoạt động không.

**4. Kiểm tra thiết bị lưu trữ**: POST kiểm tra các ổ cứng và thiết bị khác để đảm bảo chúng phản hồi đúng.

**5. Kiểm tra bàn phím và chuột**: POST đảm bảo rằng bàn phím và chuột đã được kết nối.

**6. **Khởi tạo BIOS bổ sung**: POST khởi tạo bất kỳ BIOS bổ sung nào (nếu có).

## Reading the Partition Table

Sau khi BIOS hoàn thành các kiểm tra POST, chức năng chính tiếp theo là xác định thiết bị nào sẽ được sử dụng để khởi động hệ điều hành. BIOS có thể đọc thông tin khởi động từ nhiều thiết bị khác nhau và sẽ khởi động từ thiết bị đầu tiên cung cấp phản hồi thành công. Thứ tự các thiết bị quét có thể được thiết lập trong cài đặt BIOS.

**Các thiết bị khởi động mà BIOS có thể đọc:**

1. Đĩa mềm (Floppy disks)
2. CD-ROMs
3. USB flash drives
4. Ổ cứng (Hard drives)
5. Mạng (Network)

### Định dạng bảng phân vùng:

Có hai định dạng bảng phân vùng riêng biệt: Master Boot Record (MBR) và GUID Partition Table (GPT). Cả hai định dạng này lưu trữ dữ liệu về những gì có trên ổ đĩa và được sử dụng để khởi động hệ điều hành.

* **Master Boot Record (MBR) - Cách cũ** 

    Khi BIOS đã xác định được ổ đĩa cần khởi động, nó sẽ nhìn vào sector đầu tiên trên ổ đĩa đó. Sector này chứa Master Boot Record.
  
  * **Cấu trúc MBR:**

    **1. Khối thông tin boot loader (448 bytes)**: Đây là nơi lưu trữ chương trình đầu tiên mà máy tính có thể chạy.

    **2. Bảng phân vùng (64 bytes)**: Lưu trữ thông tin về cách ổ đĩa được phân chia logic.

    MBR chỉ chiếm 512 bytes đầu tiên của không gian ổ đĩa (kích thước của một sector vật lý). Điều này giới hạn khả năng của chương trình boot loader. Khi hệ thống ngày càng phức tạp, việc "chain boot loading" đã trở nên cần thiết. Chain boot loading cho phép MBR tải một chương trình khác từ nơi khác trên ổ đĩa vào bộ nhớ. Chương trình mới sau đó được thực thi và tiếp tục quá trình khởi động.

    Nếu bạn quen thuộc với Windows, bạn có thể đã thấy các ổ đĩa được gán nhãn "C:" và "D:" - đây là các phân vùng logic trên ổ đĩa, được định nghĩa trong bảng phân vùng 64 bytes.


* **GPT - The GUID Partition Table - Cách mới**

    Thiết kế của BIOS tương thích IBM là một thiết kế cũ và có những hạn chế trong thế giới phần cứng ngày nay. Để giải quyết vấn đề này, Giao diện Firmware Mở rộng Thống nhất (UEFI) đã được tạo ra, cùng với GPT, một định dạng phân vùng mới.
    
    **Ưu điểm của GPT:**
    
    * **1. ID toàn cầu (Globally-Unique ID)**: Tham chiếu một phân vùng thay vì một số phân vùng. MBR chỉ có 64 bytes để lưu trữ thông tin phân vùng - mỗi định nghĩa phân vùng là 16 bytes. Thiết kế này cho phép có số lượng phân vùng không giới hạn.

    * **2. Khả năng khởi động từ các thiết bị lưu trữ lớn hơn 2 TB**: Nhờ không gian địa chỉ lớn hơn để xác định các sector trên đĩa. MBR không có cách nào để xác định các đĩa lớn hơn 2 TB.

    * **3. Bản sao lưu của bảng phân vùng**: Bản sao này có thể được sử dụng trong trường hợp bản chính bị hỏng. Bản sao lưu được lưu trữ ở "cuối" của đĩa.

    GPT duy trì một mức độ tương thích cho phép các PC tiêu chuẩn sử dụng BIOS cũ để khởi động từ ổ đĩa có GPT.

**Quá trình đọc bảng phân vùng và khởi động hệ điều hành:**

**1. Xác định thiết bị khởi động:** BIOS quét các thiết bị theo thứ tự được thiết lập và xác định thiết bị nào có thể khởi động.

**2.Đọc bảng phân vùng:** BIOS đọc bảng phân vùng của thiết bị khởi động để xác định phân vùng khởi động chính.

   * **Với MBR:** Đọc Master Boot Code và Partition Table.

   * **Với GPT:** Đọc GPT Header và Partition Entries.

**3. Tải Boot Sector:** BIOS tải Boot Sector từ phân vùng khởi động chính.

**4. Khởi động hệ điều hành:** Boot Sector chứa mã khởi động cần thiết để bắt đầu quá trình tải hệ điều hành vào bộ nhớ và chuyển quyền điều khiển từ BIOS sang hệ điều hành.

Quá trình này đảm bảo rằng BIOS tìm và tải hệ điều hành từ thiết bị khởi động chính xác, dựa trên định dạng bảng phân vùng MBR hoặc GPT. Trình tự khởi động có thể được điều chỉnh trong BIOS để ưu tiên các thiết bị khởi động khác nhau.

## The Boothloader

Mục đích của bootloader là nạp kernel ban đầu và các module hỗ trợ vào bộ nhớ. Một trong những bootloader phổ biến là GRUB (GRand Unified Bootloader), được sử dụng bởi nhiều bản phân phối Linux hiện nay.

**Các giai đoạn của GRUB**

GRUB là một "chain bootloader," nghĩa là nó khởi tạo theo các giai đoạn.

Các giai đoạn này bao gồm:

* **Giai đoạn 1 (Stage 1):** Đây là ứng dụng rất nhỏ có thể tồn tại ở phần đầu tiên của ổ đĩa. Nó tồn tại để nạp phần tiếp theo, lớn hơn của GRUB.

* **Giai đoạn 1.5 (Stage 1.5):** Chứa các driver cần thiết để truy cập hệ thống tập tin với giai đoạn 2.

* **Giai đoạn 2 (Stage 2)**: Giai đoạn này nạp menu và các tùy chọn cấu hình cho GRUB.

### Trên ổ đĩa định dạng MBR và BIOS chuẩn

Các giai đoạn này phải nằm trong ``448 bytes`` đầu tiên của khối thông tin boot loader. Thông thường, Giai đoạn 1 và Giai đoạn 1.5 đủ nhỏ để tồn tại trong ``448 bytes`` đầu tiên. 

Chúng chứa logic thích hợp để cho phép bootloader đọc hệ thống tập tin nơi Giai đoạn 2 được đặt.

**Quá trình cụ thể**

* **Stage 1:** Được lưu trữ trong Master Boot Record (MBR), nơi này chỉ chứa 512 bytes. Stage 1 đủ nhỏ để tồn tại trong MBR và nhiệm vụ chính của nó là tải Stage 1.5.

* **Stage 1.5:** Được đặt trong không gian giữa MBR và phân vùng đầu tiên. Stage 1.5 chứa các driver cần thiết để đọc hệ thống tập tin.

* **Stage 2:** Được lưu trữ trong phân vùng chính. Nó tải menu và cấu hình GRUB, từ đó người dùng có thể chọn hệ điều hành để khởi động.

### Trên ổ đĩa định dạng GPT và UEFI

Bo mạch chủ UEFI có thể đọc hệ thống tập tin FAT32 và thực thi mã. Firmware của hệ thống tìm kiếm một tập tin hình ảnh chứa mã khởi động cho các Giai đoạn 1 và 1.5, để Giai đoạn 2 có thể được quản lý bởi hệ điều hành.

**Quá trình cụ thể**

* **Stage 1 và 1.5:** Được lưu trữ dưới dạng tệp trên phân vùng hệ thống EFI (ESP), được định dạng FAT32. UEFI firmware tìm và thực thi các tệp này.

* **Stage 2:** Tương tự như MBR, Stage 2 được nạp từ hệ thống tập tin và hiển thị menu khởi động để chọn hệ điều hành.

### Kết luận:

Quá trình này đảm bảo rằng GRUB có thể nạp kernel và các module hỗ trợ vào bộ nhớ một cách hiệu quả, cho phép hệ điều hành khởi động một cách trơn tru trên cả hệ thống BIOS cũ và UEFI hiện đại.

## Kernel và Ramdisk

**Kernel** là thành phần chính của bất kỳ hệ điều hành nào. Nó hoạt động như trung gian cấp thấp nhất giữa phần cứng trên máy tính và các ứng dụng đang chạy trên máy tính. Kernel quản lý các tài nguyên như bộ nhớ và xử lý, và cung cấp giao diện để các phần mềm khác truy cập vào các thiết bị ngoại vi thông qua driver thiết bị.

### Quá trình khởi động với Kernel và Ramdisk

**Ramdisk** (Initial RAM Filesystem) là một cách để cung cấp hỗ trợ module cho kernel trong quá trình khởi động. Việc lưu trữ tất cả các driver thiết bị có thể có trong kernel sẽ không hiệu quả. Ramdisk giải quyết vấn đề này bằng cách cho phép kernel nạp đủ driver để đọc từ hệ thống tập tin, nơi nó có thể tìm các driver thiết bị cụ thể khi cần.

**Quá trình cụ thể:**

1. **Kernel và Ramdisk được nạp vào bộ nhớ:** Sau khi GRUB hoàn thành công việc của mình, kernel và ramdisk được nạp vào bộ nhớ.

2. **Kernel khởi động:** Kernel bắt đầu khởi động và thiết lập các cấu hình cần thiết.

3. **Sử dụng Ramdisk:** Kernel sử dụng ramdisk để nạp các driver thiết bị cơ bản cần thiết để truy cập hệ thống tập tin. Ramdisk chứa một hệ thống tập tin tối thiểu và các module cần thiết để hỗ trợ phần cứng cơ bản.

4. **Nạp driver thiết bị:** Sau khi kernel có thể truy cập hệ thống tập tin, nó sẽ nạp các driver thiết bị cụ thể từ hệ thống tập tin để hỗ trợ các thiết bị khác trên hệ thống.

5. **Chuyển điều khiển sang hệ điều hành:** Kernel tiếp tục quá trình khởi động hệ điều hành bằng cách khởi động các dịch vụ và nạp các thành phần cần thiết khác.

### Lợi ích của Ramdisk

**Hiệu quả:** Ramdisk cho phép kernel nạp chỉ những driver cần thiết ban đầu để khởi động, làm cho quá trình khởi động nhanh hơn và hiệu quả hơn.

**Linh hoạt:** Kernel có thể nạp các driver thiết bị cụ thể từ hệ thống tập tin khi cần, thay vì phải chứa tất cả các driver trong bộ nhớ ngay từ đầu.

**Hỗ trợ đa dạng phần cứng:** Với khả năng nạp module từ ramdisk, kernel có thể hỗ trợ một loạt các thiết bị phần cứng khác nhau một cách dễ dàng.


## OS Kernel và Init

### Hệ thống init

**Hệ thống init** (init system) là cơ chế tổ chức để xác định thứ tự tải các dịch vụ hệ thống trong quá trình khởi động. Hệ thống init truyền thống và vẫn phổ biến nhất trong Linux được gọi là "System V init".

**Quá trình chi tiết:**

1. Kernel khởi động:

   * Sau khi GRUB nạp kernel và ramdisk vào bộ nhớ, kernel bắt đầu khởi động.
   * Kernel sử dụng ramdisk để nạp các driver thiết bị cơ bản, cho phép nó truy cập hệ thống tập tin trên ổ cứng.

2. Thực thi tiến trình đầu tiên - /bin/init:

   * Sau khi kernel có thể truy cập hệ thống tập tin, nó sẽ thực thi tiến trình đầu tiên gọi là **/bin/init**. Đây là tiến trình cha của tất cả các tiến trình khác trên hệ thống Linux và thường được gọi là "**PID 1**".

3. Init đọc tệp cấu hình /etc/inittab:

   * Init đọc tệp cấu hình **/etc/inittab** để xác định script nào sẽ được chạy để khởi tạo hệ thống.
   * **/etc/inittab** chứa tập hợp các script khác nhau dựa trên "runlevel" mong muốn của hệ thống.

## Runlevels

**Runlevel** trong Linux định nghĩa các trạng thái hoạt động khác nhau của hệ thống, mỗi trạng thái phục vụ mục đích cụ thể tùy thuộc vào nhu cầu của người dùng hoặc quản trị viên. Chúng được quản lý bởi hệ thống init (System V init hoặc các biến thể như systemd).

### Các Runlevel Thông thường

**Runlevel 0:** Tắt hệ thống.

* Runlevel này dừng hoạt động của hệ thống hoàn toàn.

**Runlevel 1:** Chế độ Single User.

* Còn được gọi là chế độ bảo trì, cung cấp môi trường tối giản với chỉ các dịch vụ cần thiết được chạy. Thường thì mạng không được kích hoạt.

* **Mục đích:** Dùng để sửa chữa hệ thống, thực hiện các nhiệm vụ bảo trì và khôi phục khi các runlevel đa người dùng bình thường không thể truy cập do sự cố.

**Runlevel 6:** Khởi động lại hệ thống.

* Khởi động lại hệ thống sau khi tắt hết các dịch vụ và sau đó khởi động lại hệ thống.

### Sự khác nhau giữa các Runlevel 2-5:

Ở các bản phân phối Linux khác nhau, ý nghĩa của các runlevel 2-5 có thể khác nhau:

* **Các bản phân phối dựa trên RedHat (như CentOS, Fedora):**
* **Runlevel 3:** Chế độ đa người dùng với môi trường console, thường ở chế độ văn bản (text mode).

* **Runlevel 5:** Chế độ đa người dùng với môi trường đồ họa và mạng (GUI), cho phép đăng nhập đồ họa.

### Đa người dùng và Chế độ Single User:

**Multiuser:** Trong các runlevel đa người dùng, hệ thống khởi động bình thường. Tất cả các dịch vụ tiêu chuẩn như SSH và HTTP daemon được khởi động theo thứ tự được định nghĩa trong hệ thống init. Các giao diện mạng, nếu được cấu hình, sẽ được kích hoạt. Nó là hoạt động bình thường khi bạn khởi động vào một runlevel đa người dùng.

**Single User:** Runlevel này chỉ có các dịch vụ tối thiểu được kích hoạt (đặc biệt là mạng không được kích hoạt), điều này làm cho nó hữu ích cho việc sửa chữa sự cố (và không nhiều hơn thế).

**Khi nào cần dùng chế độ Single User:** Khi có sự cố xảy ra: 

* ví dụ như một thiết lập của bạn làm phiền quá trình khởi động và bạn cần tắt nó đi, hoặc có thể một hệ thống tệp quan trọng bị hỏng và bạn cần chạy kiểm tra đĩa.

**Truy cập trong chế độ Single User:** Trong chế độ này, truy cập duy nhất là thông qua bảng điều khiển console, mặc dù điều này không nhất thiết phải giới hạn trong trường hợp có mặt. Truy cập bằng cách sử dụng console từ xa qua cổng nối tiếp và các thiết bị tương tự là một công cụ quản lý phổ biến cho các trung tâm dữ liệu.

## Getty

Sau khi các script khởi tạo hệ thống đã chạy xong, hệ thống sẵn sàng hiển thị cho người dùng một dòng lệnh đăng nhập. Phương pháp để làm điều này là cung cấp một dòng lệnh đăng nhập trên một "TTY" (Teletype), từ viết tắt của thiết bị đầu cuối trong các hệ điều hành dựa trên Unix. Thuật ngữ này có nguồn gốc từ thời điểm người dùng sử dụng máy Teletype kết nối qua giao tiếp chuẩn.

TTY có thể là terminal vật lý hoặc ảo, ví dụ như các bảng điều khiển ảo mà bạn có thể truy cập bằng các tổ hợp phím như ALT+F# trên một máy Linux.

**Chức năng của Getty**

**Getty** (viết tắt của "get TTY") là chương trình quản lý TTY, thường được sử dụng để liên tục khởi động ``/bin/login``. Dưới đây là cách hoạt động:

* **Khởi động ``/bin/login``**: Getty liên tục khởi động chương trình /bin/login trên một TTY.

* **Xác thực người dùng**: Khi người dùng nhìn thấy dòng lệnh đăng nhập trên TTY, họ có thể nhập tên người dùng và mật khẩu.

* **Quá trình xác thực:** ``/bin/login`` đọc các thông tin đăng nhập được nhập và xác minh chúng với cơ chế xác thực của hệ thống (ví dụ như tệp mật khẩu hoặc dịch vụ xác thực).

* **Đăng nhập thành công:** Nếu quá trình xác thực thành công, ``/bin/login`` sẽ khởi động shell ưa thích của người dùng (ví dụ như Bash, Zsh).

* **Hoàn tất quá trình khởi động và đăng nhập:** Sau khi người dùng đã đăng nhập thành công và shell được khởi động, quá trình khởi động và đăng nhập được coi là hoàn tất.

# END

