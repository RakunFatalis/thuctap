# VLAN

# MỤC LỤC

- [VLAN](#vlan)
- [MỤC LỤC](#mục-lục)
  - [I. VLAN là gì?](#i-vlan-là-gì)
  - [II. Phân loại VLAN](#ii-phân-loại-vlan)
  - [III. Ưu và nhược điểm của VLAN](#iii-ưu-và-nhược-điểm-của-vlan)
    - [A. Ưu điểm của VLAN](#a-ưu-điểm-của-vlan)
    - [B. Nhược điểm của VLAN](#b-nhược-điểm-của-vlan)
- [END](#end)

## I. VLAN là gì?

VLan (Virtual Local Area Network) là một công nghệ mạng cho phép chia một mạng vật lý thành nhiều mạng logic, độc lập nhau trên cùng một hạ tầng vật lý. Bằng cách này, các thiết bị trong cùng một VLan có thể giao tiếp với nhau nhưng không thể giao tiếp trực tiếp với các thiết bị ở các VLan khác mà không thông qua các thiết bị định tuyến hoặc chuyển mạch mạng.

VLan được sử dụng phổ biến trong các môi trường mạng lớn để phân chia và quản lý mạng hiệu quả, đồng thời cũng giúp tăng tính bảo mật và khả năng quản lý trong hạ tầng mạng.

![](/img/vlan.jpg)

## II. Phân loại VLAN

1. **Port-based VLAN (VLAN Dựa Trên Cổng)**

    Port-based VLAN là cách cấu hình VLAN đơn giản và phổ biến nhất. Trong cách cấu hình này, mỗi cổng của switch được gắn với một VLAN xác định. Điều này có nghĩa là bất cứ thiết bị nào được kết nối vào cổng đó sẽ thuộc về VLAN tương ứng.

   * **Ưu điểm**
    
        Dễ dàng cấu hình và quản lý.

        Trực quan và dễ hiểu cho các quản trị viên mạng.

   * **Nhược điểm**:

        Khi thiết bị di chuyển sang cổng khác, cần cấu hình lại cổng đó để thiết bị vẫn thuộc cùng một VLAN.

2. **MAC address-based VLAN (VLAN Dựa Trên Địa Chỉ MAC)**

    MAC address-based VLAN là cách cấu hình mà mỗi địa chỉ MAC của thiết bị được gắn với một VLAN xác định. Điều này có nghĩa là thiết bị sẽ luôn thuộc về VLAN đó, bất kể nó được kết nối vào cổng nào của switch.

    * **Ưu điểm:**
    
        Thiết bị vẫn giữ nguyên VLAN khi di chuyển giữa các cổng khác nhau trên switch.

    * **Nhược điểm:**

        Khó quản lý hơn vì cần cấu hình và theo dõi từng địa chỉ MAC.

        Không thực tế khi số lượng thiết bị lớn và thường xuyên thay đổi.

3. **Protocol-based VLAN (VLAN Dựa Trên Giao Thức)**

    Protocol-based VLAN là cách cấu hình mà mỗi giao thức hoặc địa chỉ IP logic được gắn với một VLAN xác định. Điều này có nghĩa là các thiết bị sử dụng cùng một giao thức sẽ được gắn vào cùng một VLAN.

    * **Ưu điểm:**

        Phân đoạn mạng dựa trên loại lưu lượng hoặc giao thức, giúp tối ưu hóa và bảo mật mạng.
    
    * **Nhược điểm:**

        Phức tạp hơn trong cấu hình và quản lý.

        Ít phổ biến hơn vì sự tiện lợi của giao thức DHCP.

## III. Ưu và nhược điểm của VLAN

### A. Ưu điểm của VLAN

1. **Bảo Mật Nâng Cao**
    
    * Cô Lập Lưu Lượng Mạng: VLAN cho phép cô lập lưu lượng mạng giữa các nhóm người dùng hoặc các loại lưu lượng khác nhau. Điều này giúp ngăn chặn việc truy cập trái phép và giảm nguy cơ tấn công từ nội bộ.

    * Kiểm Soát Truy Cập: Bạn có thể thiết lập các chính sách bảo mật chi tiết hơn cho từng VLAN, giúp kiểm soát truy cập mạng hiệu quả hơn.

2. **Tăng Hiệu Quả Sử Dụng Băng Thông**

    * Giảm Lưu Lượng Broadcast: Bằng cách chia mạng thành các VLAN nhỏ hơn, lưu lượng broadcast chỉ giới hạn trong mỗi VLAN, không lan truyền khắp mạng. Điều này giảm tải cho mạng và cải thiện hiệu suất.

    * Tối Ưu Hóa Lưu Lượng: VLAN cho phép phân tách lưu lượng mạng theo từng loại dịch vụ, giúp tối ưu hóa việc sử dụng băng thông và tăng hiệu quả truyền tải.

3. **Quản Lý Mạng Dễ Dàng Hơn**

    * Cấu Trúc Mạng Linh Hoạt: VLAN cho phép tạo ra các cấu trúc mạng logic mà không cần thay đổi cấu trúc vật lý. Điều này giúp quản lý và triển khai mạng dễ dàng hơn, đặc biệt khi có sự thay đổi hoặc mở rộng mạng.

    * Phân Chia Nhóm Người Dùng: Bạn có thể dễ dàng phân chia mạng thành các nhóm người dùng khác nhau dựa trên chức năng hoặc phòng ban, giúp quản lý và theo dõi mạng hiệu quả hơn.

4. **Hiệu Quả Chi Phí**

    * Giảm Chi Phí Thiết Bị: Với VLAN, bạn có thể tạo nhiều mạng logic trên cùng một hạ tầng vật lý, giảm nhu cầu mua thêm thiết bị mạng như switch và router.

    * Tận Dụng Tối Đa Tài Nguyên Hiện Có: VLAN giúp tận dụng tối đa các thiết bị và tài nguyên hiện có mà không cần đầu tư thêm hạ tầng mạng mới.

5. **Tăng Khả Năng Mở Rộng và Linh Hoạt**

    * Dễ Dàng Mở Rộng: Khi mạng mở rộng, bạn có thể dễ dàng thêm VLAN mới hoặc điều chỉnh các VLAN hiện có mà không ảnh hưởng đến toàn bộ mạng.

    * Linh Hoạt Trong Cấu Hình: VLAN cung cấp khả năng cấu hình linh hoạt, cho phép dễ dàng thay đổi và điều chỉnh cấu trúc mạng theo nhu cầu kinh doanh.

### B. Nhược điểm của VLAN

Mặc dù VLAN mang lại nhiều lợi ích trong việc quản lý và tối ưu hóa mạng, nhưng cũng có một số nhược điểm cần cân nhắc:

1. **Bảo Mật Nâng Cao**

   * Cô Lập Lưu Lượng Mạng: VLAN cho phép cô lập lưu lượng mạng giữa các nhóm người dùng hoặc các loại lưu lượng khác nhau. Điều này giúp ngăn chặn việc truy cập trái phép và giảm nguy cơ tấn công từ nội bộ.

   * Kiểm Soát Truy Cập: Bạn có thể thiết lập các chính sách bảo mật chi tiết hơn cho từng VLAN, giúp kiểm soát truy cập mạng hiệu quả hơn.

2. **Tăng Hiệu Quả Sử Dụng Băng Thông**

   * Giảm Lưu Lượng Broadcast: Bằng cách chia mạng thành các VLAN nhỏ hơn, lưu lượng broadcast chỉ giới hạn trong mỗi VLAN, không lan truyền khắp mạng. Điều này giảm tải cho mạng và cải thiện hiệu suất.

   * Tối Ưu Hóa Lưu Lượng: VLAN cho phép phân tách lưu lượng mạng theo từng loại dịch vụ, giúp tối ưu hóa việc sử dụng băng thông và tăng hiệu quả truyền tải.

3. **Quản Lý Mạng Dễ Dàng Hơn**

   * Cấu Trúc Mạng Linh Hoạt: VLAN cho phép tạo ra các cấu trúc mạng logic mà không cần thay đổi cấu trúc vật lý. Điều này giúp quản lý và triển khai mạng dễ dàng hơn, đặc biệt khi có sự thay đổi hoặc mở rộng mạng.

   * Phân Chia Nhóm Người Dùng: Bạn có thể dễ dàng phân chia mạng thành các nhóm người dùng khác nhau dựa trên chức năng hoặc phòng ban, giúp quản lý và theo dõi mạng hiệu quả hơn.

4. **Hiệu Quả Chi Phí**
   * Giảm Chi Phí Thiết Bị: Với VLAN, bạn có thể tạo nhiều mạng logic trên cùng một hạ tầng vật lý, giảm nhu cầu mua thêm thiết bị mạng như switch và router.

   * Tận Dụng Tối Đa Tài Nguyên Hiện Có: VLAN giúp tận dụng tối đa các thiết bị và tài nguyên hiện có mà không cần đầu tư thêm hạ tầng mạng mới.

5. **Tăng Khả Năng Mở Rộng và Linh Hoạt**

   * Dễ Dàng Mở Rộng: Khi mạng mở rộng, bạn có thể dễ dàng thêm VLAN mới hoặc điều chỉnh các VLAN hiện có mà không ảnh hưởng đến toàn bộ mạng.

   * Linh Hoạt Trong Cấu Hình: VLAN cung cấp khả năng cấu hình linh hoạt, cho phép dễ dàng thay đổi và điều chỉnh cấu trúc mạng theo nhu cầu kinh doanh.

# END