# ROUTE


# MỤC LỤC
- [ROUTE](#route)
- [MỤC LỤC](#mục-lục)
  - [I. Định tuyến là gì?](#i-định-tuyến-là-gì)
  - [II. Tại sao lại cần định tuyến](#ii-tại-sao-lại-cần-định-tuyến)
  - [III. Router là gì?](#iii-router-là-gì)
  - [IV. Cách định tuyến hoạt động](#iv-cách-định-tuyến-hoạt-động)
  - [V. Các loại định tuyến chính.](#v-các-loại-định-tuyến-chính)
    - [Định tuyến tĩnh (Static routing):](#định-tuyến-tĩnh-static-routing)
    - [Định tuyến động (Dynamic routing):](#định-tuyến-động-dynamic-routing)
- [END](#end)

## I. Định tuyến là gì?

Định tuyến (Routing) là một công việc thường được diễn ra trên thiết bị Router nhằm tìm ra đường dẫn tốt nhất để chuyển tiếp dữ liệu từ một thiết bị nguồn tới một thiết bị đích. Đường dẫn tốt nhất ở đây có thể hiểu là đường dẫn mà tốn ít thời gian nhất hoặc đường dẫn có thể sử dụng duy nhất.

![](/img/route.png)


Theo ảnh trên, Máy tính A muốn nhắn tin cho máy tính B có thể đi theo 2 đường dẫn:

* Đường 1: đi qua mạng 1, 3 và 5
* Đường 2: đi qua mạng 2 và 4.

Khi dữ liệu từ máy tính A đến Router nó sẽ phân tích và quyết định lựa chọn đường dẫn tốt nhất trong 2 đường dẫn. Trong trường hợp này, Router sẽ chọn đường 1 vì đường truyền từ mạng 2 đến mạng 4 bị chậm.

Mặc dù Router thường đảm nhiệm vị trí thực hiện việc định tuyến nhưng loại Switch Layer 3 cũng có thể thực hiện nhiệm vụ này. Loại bộ chuyển mạch này dùng để định tuyến dữ liệu giữa nhiều mạng con với nhau trong một mạng lớn hơn.

## II. Tại sao lại cần định tuyến

Routing là một khía cạnh quan trọng của mạng máy tính vì nó tạo ra sự hiệu quả trong giao tiếp mạng. Khi không có hệ thống định tuyến đúng đắn, các vấn đề có thể xảy ra như thời gian chờ đợi lâu khi người dùng truy cập các trang web, hoặc các máy chủ web có thể bị quá tải và gây ra sự cố khi không thể xử lý được số lượng người dùng lớn.

Định tuyến giúp giảm thiểu các sự cố mạng bằng cách quản lý lưu lượng dữ liệu sao cho mạng có thể sử dụng hết khả năng của mình mà không gây tắc nghẽn. Bằng cách định tuyến thông minh, dữ liệu được chuyển đi đúng hướng và đến đích một cách nhanh chóng và hiệu quả nhất. Điều này cải thiện trải nghiệm người dùng và đảm bảo rằng các dịch vụ mạng có thể hoạt động một cách trơn tru và ổn định.

Việc triển khai hệ thống định tuyến hiệu quả cũng giúp tối ưu hóa tài nguyên mạng, giảm thiểu chi phí hoạt động và nâng cao khả năng mở rộng của hạ tầng mạng. Do đó, định tuyến không chỉ đơn giản là điều quan trọng mà là một yếu tố cốt lõi để đảm bảo hoạt động hiệu quả của mạng và các dịch vụ trực tuyến ngày nay.

## III. Router là gì?

Một router là thiết bị mạng kết nối các thiết bị tính toán và mạng với các mạng khác. Router chủ yếu thực hiện ba chức năng chính:

* **Xác định đường đi (Path determination)**:

    Router xác định đường đi dữ liệu sẽ đi từ nguồn đến đích. Nó cố gắng tìm ra đường đi tốt nhất bằng cách phân tích các yếu tố mạng như độ trễ, dung lượng và tốc độ.

* **Chuyển tiếp dữ liệu (Data forwarding)**:

Router chuyển tiếp dữ liệu đến thiết bị tiếp theo trên đường đi đã chọn để cuối cùng đạt được đích đến. Thiết bị và router có thể thuộc cùng một mạng hoặc các mạng khác nhau.

* **Cân bằng tải (Load balancing)**:

    Đôi khi router có thể gửi các bản sao của cùng một gói dữ liệu qua nhiều đường đi khác nhau. Điều này giúp giảm thiểu lỗi do mất mát dữ liệu, tạo ra tính dự phòng và quản lý khối lượng lưu lượng mạng.


Router là một thành phần quan trọng của hạ tầng mạng, đảm bảo các thiết bị trong mạng có thể giao tiếp với nhau và với Internet một cách hiệu quả. Bằng cách xác định và chuyển tiếp dữ liệu thông minh, router giúp cải thiện trải nghiệm người dùng và đảm bảo hoạt động ổn định của mạng. Cân bằng tải cũng đóng vai trò quan trọng trong việc phân phối tài nguyên mạng một cách hiệu quả và đảm bảo sự liên tục của dịch vụ.

## IV. Cách định tuyến hoạt động

* **Gói dữ liệu và tiêu đề (Data packets and headers)**:

    Dữ liệu di chuyển trong mạng thông qua các gói dữ liệu. Mỗi gói dữ liệu có một tiêu đề chứa thông tin về đích đến dự kiến của gói dữ liệu đó. Tiêu đề này chứa các thông tin như địa chỉ IP của nguồn và đích, cùng các thông tin khác như số thứ tự gói dữ liệu, chiều dài và kiểu dữ liệu.

* **Quá trình định tuyến (Routing process)**:

    Khi một gói dữ liệu đến một router, router đầu tiên sẽ kiểm tra tiêu đề của gói dữ liệu này. Điều này tương tự như khi một hành khách kiểm tra lịch trình xe buýt để tìm tuyến xe tốt nhất đến đích.

* **Bảng định tuyến (Routing table)**:

    Router sử dụng các bảng định tuyến để quyết định điều hướng gói dữ liệu. Bảng này chứa các thông tin về các mạng và địa chỉ IP mà router biết đến, cùng với các giao diện mạng nào để sử dụng để đến được các mạng đó.

* **Chuyển tiếp dữ liệu (Data forwarding)**:

    Sau khi router xác định đích đến của gói dữ liệu từ bảng định tuyến, nó tiến hành chuyển tiếp gói dữ liệu tới đích tiếp theo trên mạng. Điều này có thể là một router tiếp theo trong chuỗi định tuyến, hoặc đến thiết bị như máy in hay thiết bị khác trong mạng nội bộ.

Quá trình định tuyến xảy ra với tốc độ cực kỳ nhanh và liên tục trong mạng, giúp cho dữ liệu di chuyển một cách hiệu quả và đáp ứng nhanh chóng yêu cầu của người dùng. Điều này làm cho hệ thống mạng trở nên linh hoạt và khả năng mở rộng.

## V. Các loại định tuyến chính.

### Định tuyến tĩnh (Static routing):

Trong định tuyến tĩnh, một nhà quản trị mạng sử dụng các bảng tĩnh để cấu hình và lựa chọn các đường đi mạng. Định tuyến tĩnh hữu ích trong các tình huống mà thiết kế mạng hoặc các tham số được dự kiến sẽ không thay đổi.

Tính tĩnh của kỹ thuật định tuyến này đi kèm với các hạn chế dự kiến, chẳng hạn như tắc nghẽn mạng. Mặc dù nhà quản trị có thể cấu hình các đường dự phòng trong trường hợp một liên kết bị lỗi, định tuyến tĩnh nói chung làm giảm tính linh hoạt và sự thích ứng của mạng, dẫn đến hiệu suất mạng bị hạn chế.

### Định tuyến động (Dynamic routing):

Trong định tuyến động, các router tạo và cập nhật bảng định tuyến vào thời điểm chạy dựa trên các điều kiện mạng thực tế. Chúng cố gắng tìm đường đi nhanh nhất từ nguồn đến đích bằng cách sử dụng một giao thức định tuyến động, đó là một tập hợp các quy tắc tạo ra, duy trì và cập nhật bảng định tuyến động.

Ưu điểm lớn nhất của định tuyến động là nó thích nghi với các điều kiện mạng thay đổi, bao gồm lưu lượng, băng thông và sự cố mạng.

# END