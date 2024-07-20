# VPN

# Mục lục

- [VPN](#vpn)
- [Mục lục](#mục-lục)
  - [1. VPN là gì?](#1-vpn-là-gì)
  - [2. VPN hoạt động ra sao?](#2-vpn-hoạt-động-ra-sao)
  - [3. Các lợi ích khi dùng VPN](#3-các-lợi-ích-khi-dùng-vpn)
- [END](#end)

## 1. VPN là gì?

VPN (Virtual Private Network - Mạng riêng ảo) là công nghệ cung cấp cho người dùng khả năng truy cập vào một mạng riêng (LAN) của các máy tính cá nhân và máy chủ trong mạng riêng đó từ một điểm bên ngoài của mạng đó, và không làm ảnh hưởng đến an ninh bảo mật của mạng đó.

VPN che giấu địa chỉ public IP thực của người dùng và tunnel cho lưu lượng dữ liệu giữa thiết bị của người dùng và máy chủ từ xa. Đa số người dùng đăng ký dịch vụ VPN để tránh bị theo dõi trực tuyến, và họ thường sử dụng VPN khi kết nối với mạng Wi-Fi công cộng, nơi có nguy cơ lớn đối với sự an toàn của dữ liệu của họ

## 2. VPN hoạt động ra sao?

VPN (Virtual Private Network) hoạt động bằng cách tạo ra một kết nối mạng ảo, được mã hóa, giữa thiết bị của bạn và một máy chủ VPN. Dưới đây là cách hoạt động cơ bản của VPN:

![](/img/VPN_work.jpg)

1. **Tạo kết nối**: Khi bạn kết nối với một VPN, ứng dụng VPN trên thiết bị của bạn sẽ thiết lập một kết nối mã hóa với một máy chủ VPN. Kết nối này thường được thiết lập thông qua một giao thức kết nối mạng an toàn như OpenVPN, IKEv2, hoặc L2TP/IPSec.

2. **Xác thực người dùng**: Để đảm bảo rằng chỉ những người dùng được phép mới có thể kết nối với VPN, hệ thống sẽ yêu cầu bạn xác thực thông tin người dùng của mình bằng cách nhập tên người dùng và mật khẩu hoặc sử dụng phương thức xác thực khác như mã xác minh hai yếu tố (2FA).

3. **Mã hóa dữ liệu**: Khi kết nối được thiết lập, dữ liệu của bạn sẽ được mã hóa trước khi nó rời khỏi thiết bị của bạn và đi qua internet. Quá trình mã hóa này giúp bảo vệ dữ liệu của bạn khỏi những kẻ nghe trộm và hacker.

4. **Gửi dữ liệu đến máy chủ VPN**: Dữ liệu đã mã hóa sẽ được gửi đến máy chủ VPN, nơi nó sẽ được giải mã và chuyển tiếp đến điểm đến cuối cùng trên internet.

5. **Nhận dữ liệu từ máy chủ VPN**: Khi dữ liệu từ internet đến máy chủ VPN, nó sẽ được mã hóa và gửi trở lại thiết bị của bạn. Thiết bị của bạn sẽ giải mã dữ liệu và hiển thị nó cho bạn như bình thường.

6. **Ẩn địa chỉ IP và thay đổi vị trí**: Một trong những tính năng quan trọng của VPN là nó giúp ẩn địa chỉ IP thực của bạn và cho phép bạn chọn vị trí địa lý mà bạn muốn hiển thị. Điều này giúp bảo vệ danh tính trực tuyến của bạn và cho phép bạn truy cập vào nội dung bị giới hạn địa lý.

## 3. Các lợi ích khi dùng VPN

VPN mang lại nhiều ích lợi và lợi ích cho người dùng, dưới đây là một số lí do chính tại sao bạn nên sử dụng VPN:

1. **Bảo mật dữ liệu**: VPN mã hóa dữ liệu của bạn khi bạn truyền qua mạng internet, ngăn chặn các bên thứ ba có thể nghe trộm hoặc đánh cắp thông tin cá nhân như mật khẩu, số thẻ tín dụng và dữ liệu nhạy cảm khác.

2. **Bảo vệ địa chỉ IP**: VPN giấu địa chỉ IP thực của bạn bằng cách sử dụng địa chỉ IP của máy chủ VPN. Điều này giúp bạn duy trì sự ẩn danh trực tuyến và ngăn chặn các dịch vụ và trang web từ việc xác định vị trí của bạn.

3. **Truy cập vào nội dung địa phương**: Bằng cách kết nối đến một máy chủ VPN ở một quốc gia khác, bạn có thể truy cập vào nội dung trên internet mà có thể bị giới hạn địa lý, như các dịch vụ phim trực tuyến, truyền hình và trang web.

4. **Bảo vệ khi sử dụng Wi-Fi công cộng**: Khi sử dụng Wi-Fi công cộng, dữ liệu của bạn có thể dễ dàng bị đánh cắp. VPN cung cấp một kết nối bảo mật, ngăn chặn tin tặc mạng từ việc truy cập vào dữ liệu cá nhân của bạn.

5. **Bảo vệ quyền riêng tư trực tuyến**: VPN giúp bảo vệ quyền riêng tư của bạn bằng cách ngăn chặn các tổ chức, công ty hoặc chính phủ từ việc theo dõi và thu thập thông tin về hành vi trực tuyến của bạn.

6. **An toàn khi làm việc từ xa**: Nếu bạn làm việc từ xa và cần truy cập vào mạng nội bộ của công ty, VPN cung cấp một kết nối an toàn để bạn có thể làm việc một cách an toàn và bảo mật.

# END