# STATIC VÀ DYNAMIC ROUTE

# MỤC LỤC


## I. Static route

### 1. Static route là gì?

Static Route là một phương pháp định tuyến trong mạng máy tính mà các tuyến đường được cấu hình thủ công bởi người quản trị mạng. Khác với định tuyến động (dynamic routing) mà các bảng định tuyến tự động cập nhật dựa trên các thông tin định tuyến, Static Route yêu cầu người quản trị phải thủ công nhập các tuyến đường cụ thể vào bảng định tuyến của thiết bị mạng.

Mặc dù Static Route không linh hoạt như các phương pháp định tuyến động, nhưng nó mang lại nhiều lợi ích đáng kể. Một trong những lợi ích chính là tính đáng tin cậy. Vì các tuyến đường được cấu hình thủ công, nên chúng thường ổn định hơn trong môi trường mạng ít thay đổi. Điều này giúp giảm thiểu các vấn đề có thể xảy ra do sự không đồng nhất hoặc lỗi cập nhật định tuyến.

### 2. Lợi ích và hạn chế của Static Route

**Lợi ích:**

* Đơn giản và dễ triển khai: Cấu hình và triển khai Static Route rất dễ dàng, không đòi hỏi sự tự động cập nhật như định tuyến động.
* Đáng tin cậy và ổn định: Do tuyến đường được cấu hình thủ công, nên chúng có xu hướng ổn định hơn trong môi trường mạng ít thay đổi.
* Kiểm soát cao: Người quản trị có toàn quyền kiểm soát việc chuyển tiếp dữ liệu trên mạng thông qua việc cấu hình tuyến đường cụ thể.
* Hiệu suất tốt trong mạng nhỏ và trung bình: Trong các mạng có quy mô nhỏ và trung bình, việc sử dụng Static Route có thể mang lại hiệu suất tốt hơn so với định tuyến động.

**Hạn chế:**

* Không linh hoạt trong mạng lớn và phức tạp: Trong các mạng lớn và phức tạp, việc cấu hình và duy trì các tuyến đường tĩnh trở nên không hiệu quả và phức tạp.

* Khả năng mở rộng hạn chế: Static Route không thích hợp cho các mạng có sự mở rộng nhanh chóng hoặc có nhu cầu thay đổi định tuyến thường xuyên.

### 3. Ứng dụng của định tuyến tĩnh

* **Kết nối các mạng riêng biệt**: Định tuyến tĩnh có thể được sử dụng để kết nối các mạng riêng biệt không có kết nối trực tiếp với nhau, ví dụ như kết nối mạng LAN của công ty với mạng của nhà cung cấp dịch vụ Internet (ISP).

* **Điều khiển lưu lượng truy cập**: Định tuyến tĩnh cho phép người dùng điều khiển lưu lượng truy cập theo một cách cụ thể, ví dụ như ưu tiên lưu lượng truy cập đến một số mạng nhất định hoặc hạn chế truy cập đến các mạng nhạy cảm.

* **Tăng cường bảo mật**: Định tuyến tĩnh có thể được sử dụng để tăng cường bảo mật mạng bằng cách hạn chế truy cập đến các mạng nội bộ hoặc các dịch vụ nhạy cảm.

### 4. Câu lệnh static route

Câu lệnh để cấu hình static route có thể khác nhau tùy vào hệ điều hành và thiết bị mạng bạn đang sử dụng. Dưới đây là một số ví dụ về cách cấu hình static route trên một số hệ điều hành phổ biến:

* **Trên Windows (Command Prompt):**

    **Để thêm một static route**: ``route add <đích_mạng> mask <subnet_mask> <gateway>``

    Ví dụ: ``route add 192.168.2.0 mask 255.255.255.0 192.168.1.1``

    **Để xóa một static route đã cấu hình:** ``route delete <đích_mạng>``

* **Trên Linux (Terminal):**

    **Để thêm một static route**: ``sudo ip route add <đích_mạng>/<subnet_mask> via <gateway>``

    Ví dụ: ``sudo ip route add 192.168.2.0/24 via 192.168.1.1``

    **Để xóa một static route đã cấu hình:** ``sudo ip route del <đích_mạng>/<subnet_mask>``

## II. Dynamic route

### 1. Dynamic route là gì?

Dynamic route là một phương pháp định tuyến trong mạng máy tính mà các định tuyến được tự động cập nhật và quản lý bởi các giao thức định tuyến. Các giao thức này cho phép các thiết bị mạng trao đổi thông tin về mạng và điều chỉnh bảng định tuyến của mình một cách tự động dựa trên các thay đổi trong mạng, như thêm mới các đường đi hay cập nhật thông tin về các đường đi hiện có.

### 2. Lợi ích và hạn chế của Dynamic Route

**Lợi ích**

* **Tự động cập nhật**: Các định tuyến được tự động cập nhật và điều chỉnh dựa trên thông tin mạng thay đổi. Điều này giúp mạng linh hoạt hơn và dễ dàng mở rộng khi có thêm thiết bị hoặc mạng con mới.

* **Phát hiện lỗi và khôi phục**: Các giao thức định tuyến động thường có khả năng phát hiện lỗi và khôi phục nhanh chóng khi có sự cố xảy ra trong mạng. Chúng có thể tự động chuyển hướng lưu lượng qua các đường đi thay thế để đảm bảo tính liên lạc liên tục.

* **Tiết kiệm thời gian và công sức**: Không cần phải cấu hình thủ công từng đường đi, giúp tiết kiệm thời gian và giảm thiểu sai sót con người.

* **Phù hợp với mạng lớn và phức tạp**: Dynamic routing thích hợp cho các mạng lớn và phức tạp, nơi có nhiều thiết bị và đường đi khác nhau cần phải tự động quản lý và điều phối.

**Hạn chế**

* **Yêu cầu tài nguyên tính toán**: Các giao thức định tuyến động yêu cầu tài nguyên tính toán để duy trì và chuyển đổi thông tin định tuyến. Điều này có thể tạo ra tải cho các thiết bị mạng, đặc biệt là trong các mạng lớn.

* **Khả năng thích ứng chậm**: Các giao thức định tuyến động có thể không phản ứng nhanh đủ để thích ứng với các thay đổi nhỏ trong mạng, so với các cấu hình static route được cấu hình thủ công một cách cụ thể.

* **Bảo mật và quản lý rủi ro**: Dynamic routing có thể tạo ra các lỗ hổng bảo mật nếu không được cấu hình và quản lý chặt chẽ. Các giao thức định tuyến động phải được bảo mật để tránh bị tấn công hoặc lạm dụng.

* **Phức tạp khi triển khai**: So với static routing, dynamic routing có thể phức tạp hơn trong việc triển khai và quản lý, đặc biệt là đối với những người quản trị mạng không có nhiều kinh nghiệm.

## III. Sự khác nhau giữa 2 loại định tuyến

| Đặc điểm| Định tuyến tĩnh | Định tuyến động |
|----|--------------|-------------------|
| Routes  | Các đường đi được người dùng xác định | Được cập nhật theo định hướng mạng |
| Thuật toán định tuyến  | Không sử dụng thuật toán phức tạp| Sử dụng các thuật toán định tuyến phức tạp|
| Bảo mật| Cung cấp bảo mật cao | Cung cấp bảo mật thấp|
| Tự động hóa | Thủ công | Tự động|
| Kích thước hệ thống mạng | Mạng nhỏ | Mạng lớn |
| Yêu cầu tài nguyên | Yêu cầu ít tài nguyên bổ sung | Yêu cầu tài nguyên bổ sung  |
| Lỗi kết nối | Gây gián đoạn định tuyến khi có lỗi kết nối | Không làm gián đoạn định tuyến khi có lỗi kết nối |
| Băng thông | Yêu cầu ít băng thông | Yêu cầu nhiều băng thông|
| Cấu hình | Khó để cấu hình  | Dễ dàng để cấu hình  |

