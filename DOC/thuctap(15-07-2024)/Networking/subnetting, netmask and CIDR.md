# SUBNETTING, NETMASK AND CIDR

# MỤC LỤC


## I. SUBNETTING

### 1. Subnetting là gì

Subnetting là quá trình phân chia một mạng lớn (một dải địa chỉ IP) thành các mạng con nhỏ hơn. Điều này không chỉ giúp tối ưu hóa việc sử dụng địa chỉ IP mà còn giúp cải thiện hiệu suất và bảo mật của mạng.

### 2. Tại sao lại cần subnetting.

Mỗi doanh nghiệp đều cần một cách thiết kế mạng hiệu quả để truyền dữ liệu trơn tru và không lỗi qua kênh mạng.

Để khắc phục vấn đề sử dụng quá nhiều ID mạng, khái niệm chia mạng con được áp dụng trong hệ thống. Để hiểu điều này, hãy xem một số lý do sử dụng chia mạng con:

1. **Mạng con (Sub-network)**:

   * **Phân phối địa chỉ IP hiệu quả**: Subnetting giúp phân chia một dải địa chỉ IP lớn thành nhiều subnet nhỏ hơn theo nhu cầu cụ thể của mạng. Điều này giúp tổ chức các thiết bị trong mạng một cách hợp lý và hiệu quả.
   
   * **Quản lý dễ dàng**: Việc chia mạng thành các subnet nhỏ hơn giúp việc quản lý và giám sát trở nên dễ dàng hơn. 

2. **Tăng cường bảo mật (Increased Security)**:

   * **Thiết lập đơn vị bảo mật**: Subnetting giúp dễ dàng thiết lập các khu vực bảo mật riêng biệt trong mạng. Mỗi subnet có thể có các chính sách bảo mật và quyền truy cập riêng, giúp bảo vệ dữ liệu khỏi các vi phạm.
   
   * **Cô lập sự cố**: Khi có sự cố xảy ra, subnetting giúp cô lập và giải quyết vấn đề trong một subnet cụ thể mà không ảnh hưởng đến toàn bộ mạng.

3. **Ngăn chặn lãng phí địa chỉ IP (Prevent wastage of IP addresses)**:

   * **Sử dụng hiệu quả tài nguyên**: Bằng cách chia nhỏ mạng thành các subnet, subnetting giúp sử dụng địa chỉ IP một cách hiệu quả hơn, tránh lãng phí tài nguyên địa chỉ IP có sẵn.

4. **Giao tiếp tốt hơn giữa các mạng con (Better communication between subnets)**:
   
   * **Tối ưu hóa giao tiếp**: Subnetting giúp tối ưu hóa giao tiếp giữa các subnet, đảm bảo rằng dữ liệu được truyền một cách hiệu quả và nhanh chóng.
   
   * **Cải thiện hiệu suất mạng**: Việc chia mạng thành các subnet nhỏ hơn giúp giảm thiểu tắc nghẽn và cải thiện hiệu suất tổng thể của mạng.