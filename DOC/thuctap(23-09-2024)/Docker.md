# Docker

# Mục lục


- [Docker](#docker)
- [Mục lục](#mục-lục)
- [I. Docker là gì ?](#i-docker-là-gì-)
  - [1. Giới thiệu Docker](#1-giới-thiệu-docker)
  - [2. Vì sao phải dùng Docker.](#2-vì-sao-phải-dùng-docker)
- [II. Hoạt động của Container](#ii-hoạt-động-của-container)
  - [1. Container là gì.](#1-container-là-gì)
  - [2. Container với máy ảo(VM).](#2-container-với-máy-ảovm)
- [III. Hệ sinh thái Docker](#iii-hệ-sinh-thái-docker)
  - [1. Docker Network](#1-docker-network)
  - [2. Docker Image](#2-docker-image)
  - [3. Docker Volume](#3-docker-volume)
  - [4. Docker Compose](#4-docker-compose)
  - [5. Docker Swarm](#5-docker-swarm)
- [END](#end)

# I. Docker là gì ?

## 1. Giới thiệu Docker

Docker là một nền tảng mở để phát triển, triển khai, và chạy các ứng dụng. Với Docker, bạn có thể tách biệt các ứng dụng khỏi cơ sở hạ tầng, giúp việc phát triển và triển khai phần mềm trở nên nhanh chóng hơn. Docker cho phép quản lý cơ sở hạ tầng theo cách giống như bạn quản lý ứng dụng, nhờ vậy tối ưu hóa quá trình triển khai.

Bằng cách sử dụng các phương pháp của Docker trong việc đóng gói, kiểm thử, và triển khai mã nguồn, bạn có thể giảm thiểu thời gian trễ giữa việc viết mã và đưa nó vào môi trường sản xuất. Docker giúp tăng tốc quy trình làm việc và đảm bảo tính nhất quán trong việc triển khai ứng dụng ở mọi môi trường, từ máy tính cá nhân đến hệ thống máy chủ đám mây.

## 2. Vì sao phải dùng Docker.

**A. Phân phối ứng dụng của bạn nhanh chóng và nhất quán.**

Docker là một công cụ mạnh mẽ giúp quản lý các container - môi trường ảo hóa nhẹ chứa các ứng dụng và dịch vụ. Các container giúp đảm bảo rằng ứng dụng của bạn có thể chạy nhất quán trên các môi trường khác nhau, từ máy tính cá nhân, môi trường kiểm thử, đến môi trường sản xuất. Docker được sử dụng rất nhiều trong các quy trình phát triển liên tục (CI/CD).

Ví dụ như:

* **Phát triển ứng dụng**: Các lập trình viên viết mã trên máy tính cá nhân và sử dụng Docker để đóng gói mã vào container. Mọi thứ trong container sẽ giống nhau bất kể họ đang sử dụng hệ điều hành hay môi trường nào, giúp việc chia sẻ công việc với đồng nghiệp trở nên dễ dàng.

* **Kiểm thử**: Sau khi mã được đóng gói, ứng dụng sẽ được đẩy vào môi trường kiểm thử. Tại đây, Docker sẽ giúp chạy các bài kiểm thử tự động và thủ công để đảm bảo tính ổn định.

* **Sửa lỗi**: Khi phát hiện lỗi, lập trình viên có thể sửa lỗi trong môi trường phát triển, rồi sau đó lại đẩy bản sửa lỗi vào môi trường kiểm thử để kiểm tra lại. 

* **Triển khai sản phẩm**: Sau khi quá trình kiểm thử hoàn tất, việc đưa ứng dụng đến tay khách hàng chỉ cần đẩy container cập nhật lên môi trường sản xuất mà không phải lo về sự khác biệt giữa các môi trường.

**B. Triển khai và mở rộng linh hoạt.**

Docker cho phép triển khai và mở rộng linh hoạt thông qua nền tảng container hóa, giúp ứng dụng có thể chạy trên nhiều môi trường khác nhau như máy tính cá nhân của nhà phát triển, máy ảo hay máy chủ vật lý trong trung tâm dữ liệu, hoặc trên các nền tảng cloud.

Nhờ tính di động cao và nhẹ nhàng, Docker cho phép quản lý tải công việc một cách linh hoạt. Điều này có nghĩa là bạn có thể nhanh chóng mở rộng quy mô ứng dụng khi nhu cầu kinh doanh tăng lên, hoặc thu hẹp lại khi không cần thiết, tất cả đều diễn ra gần như ngay lập tức, đáp ứng yêu cầu thay đổi trong thời gian thực.

Tính năng này rất hữu ích trong việc triển khai ứng dụng linh hoạt, giúp tiết kiệm tài nguyên và tối ưu hiệu suất hoạt động.

**C. Chạy nhiều tác vụ hơn trên cùng một phần cứng.**

Docker nhẹ và nhanh, mang lại một giải pháp thay thế hiệu quả về chi phí so với các máy ảo dựa trên hypervisor (trình ảo hóa). Nhờ Docker, bạn có thể tận dụng được nhiều hơn dung lượng của máy chủ, từ đó đạt được các mục tiêu kinh doanh mà không cần phải đầu tư nhiều vào phần cứng.

Docker đặc biệt phù hợp trong các môi trường có mật độ cao hoặc với các triển khai vừa và nhỏ, nơi bạn cần làm nhiều việc hơn với ít tài nguyên hơn. Bởi vì container Docker không yêu cầu hệ điều hành riêng như máy ảo, bạn có thể chạy nhiều ứng dụng trên cùng một phần cứng mà không gây lãng phí tài nguyên.

# II. Hoạt động của Container

## 1. Container là gì.

Nếu bạn đang phát triển một ứng dụng web với ba thành phần chính - một frontend React, một API Python, và một cơ sở dữ liệu PostgreSQL, thì bạn sẽ cần cài đặt Node, Python và PostgreSQL.

Làm sao để bạn đảm bảo rằng bạn và các nhà phát triển khác trong nhóm của bạn đang sử dụng cùng phiên bản với nhau? Hoặc sử dụng cùng phiên bản trên hệ thống CI/CD? Hoặc phiên bản đang được dùng trong môi trường production?

Làm thế nào để đảm bảo phiên bản Python (hoặc Node hay cơ sở dữ liệu) mà ứng dụng của bạn cần không bị ảnh hưởng bởi những gì đã có trên máy của bạn? Làm sao để quản lý các xung đột tiềm ẩn?

Điều đó khiến chúng ra ra đời Container.

Container là gì? Nói đơn giản, container là các tiến trình cách ly cho từng thành phần của ứng dụng của bạn. Mỗi thành phần - ứng dụng React frontend, engine API Python, và cơ sở dữ liệu - chạy trong môi trường riêng biệt, hoàn toàn tách biệt với mọi thứ khác trên máy của bạn.

Điều làm cho container trở nên tuyệt vời là:

* **Tự chứa**: Mỗi container có mọi thứ nó cần để hoạt động mà không phụ thuộc vào bất kỳ phụ thuộc nào đã được cài đặt sẵn trên máy chủ.

* **Cách ly**: Vì các container chạy trong môi trường cách ly, chúng ít ảnh hưởng đến máy chủ và các container khác, giúp tăng cường bảo mật cho ứng dụng của bạn.

* **Độc lập**: Mỗi container được quản lý độc lập. Việc xóa một container sẽ không ảnh hưởng đến các container khác.

* **Di động**: Container có thể chạy ở bất kỳ đâu! Container chạy trên máy phát triển của bạn sẽ hoạt động tương tự trong trung tâm dữ liệu hoặc bất kỳ đâu trên đám mây!

## 2. Container với máy ảo(VM).

Một máy ảo (VM) là một hệ điều hành hoàn chỉnh với kernel riêng, driver phần cứng, chương trình, và ứng dụng của nó. Việc khởi động một VM chỉ để cô lập một ứng dụng duy nhất sẽ tạo ra rất nhiều chi phí về tài nguyên.

Trong khi đó, một container chỉ đơn giản là một tiến trình cách ly với tất cả các tệp tin cần thiết để chạy. Nếu bạn chạy nhiều container, tất cả chúng đều chia sẻ cùng một kernel, giúp bạn có thể chạy nhiều ứng dụng hơn với hạ tầng ít hơn.

Mặc dù máy ảo (VM) và container có thể hoạt động độc lập, nhưng chúng thường được sử dụng cùng nhau để tối ưu hóa tài nguyên.

Cụ thể, trong môi trường điện toán đám mây, các máy chủ bạn tạo ra thường là các máy ảo (VM). Thay vì chỉ sử dụng một VM để chạy duy nhất một ứng dụng, bạn có thể cài đặt một "container runtime" (môi trường chạy container) lên VM đó và sau đó chạy nhiều ứng dụng đóng gói trong container trên cùng một máy ảo. Điều này giúp bạn sử dụng tài nguyên hiệu quả hơn và tiết kiệm chi phí, vì bạn có thể tận dụng một VM để chạy nhiều ứng dụng thay vì tạo nhiều VM cho từng ứng dụng riêng lẻ.

# III. Hệ sinh thái Docker

## 1. Docker Network

Docker Network dùng để quản lý và thiết lập kết nối giữa các container với nhau hoặc giữa container và thế giới bên ngoài (như internet hoặc hệ thống host). Docker cung cấp nhiều tùy chọn mạng để đảm bảo container có thể giao tiếp với nhau theo cách an toàn và linh hoạt.

Có ba loại Docker Network chính:

  * **Bridge network (Mạng cầu)**: Đây là mạng mặc định khi bạn chạy một container mà không chỉ định mạng cụ thể. Các container trên cùng một bridge network có thể giao tiếp với nhau, nhưng không thể truy cập từ bên ngoài nếu không cấu hình thêm.

  * **Host network (Mạng host)**: Loại mạng này cho phép container chia sẻ cùng một network namespace với máy host, nghĩa là container sẽ sử dụng địa chỉ IP và cổng của máy host. Điều này giúp loại bỏ lớp ảo hóa mạng của Docker nhưng có thể gây ra rủi ro về bảo mật.

  * **Overlay network**: Thường được sử dụng trong Docker Swarm, overlay network cho phép các container trên các máy chủ khác nhau giao tiếp với nhau một cách an toàn. Nó tạo ra một mạng ảo trên các host Docker để các container trong cùng một Swarm có thể kết nối với nhau.

## 2. Docker Image

Docker Image là một bản mẫu không thay đổi, chứa tất cả các thông tin cần thiết để chạy một ứng dụng dưới dạng một container. Docker Image bao gồm mã nguồn của ứng dụng, thư viện, các công cụ, các phụ thuộc và thiết lập môi trường mà ứng dụng cần. Docker Image đóng vai trò như một "blueprint" (bản thiết kế) cho việc tạo ra container.

Cấu trúc của Docker Image:

  * **Layer (Lớp)**: Docker Image được xây dựng từ nhiều lớp (layer). Mỗi lớp tương ứng với một bước trong quá trình xây dựng (build) image. Khi image được cập nhật, Docker chỉ thêm các lớp mới, còn các lớp cũ không bị thay đổi, giúp tiết kiệm không gian lưu trữ.

  * **Union File System**: Docker Image sử dụng union file system để quản lý các lớp này, cho phép kết hợp nhiều lớp thành một file system duy nhất mà container có thể sử dụng.

  * **Base Image (Ảnh gốc)**: Mọi Docker Image thường được xây dựng dựa trên một base image, có thể là một hệ điều hành tối giản như Ubuntu, Alpine, hoặc từ các image đặc thù khác như Node.js, Python, v.v.

Các Docker Image thường được lưu trữ và chia sẻ qua Docker Hub hoặc các Docker Registry khác, giúp dễ dàng phân phối và sử dụng trong các môi trường khác nhau. Khi bạn chạy một container, Docker sẽ kéo image từ registry (nếu chưa có sẵn) và khởi tạo một container dựa trên image đó.

## 3. Docker Volume

Docker Volume là một cơ chế lưu trữ trong Docker, được sử dụng để lưu trữ và chia sẻ dữ liệu giữa các container hoặc giữa container và hệ thống host. Docker Volume giúp duy trì dữ liệu bất kể container bị xóa hoặc tạo lại, đảm bảo dữ liệu không bị mất khi container ngừng hoạt động.

**Có ba loại lưu trữ phổ biến trong Docker:**

  * **Volume**: Đây là phương pháp lưu trữ được Docker quản lý, tách biệt hoàn toàn khỏi hệ thống tệp của container. Volumes tồn tại độc lập so với vòng đời của container, nghĩa là khi bạn xóa container, volume vẫn tồn tại trừ khi được xóa thủ công. Volumes có thể được gắn vào nhiều container để chia sẻ dữ liệu giữa chúng.

  * **Bind mount**: Phương pháp này gắn trực tiếp một thư mục từ hệ thống host vào container. Khi bạn sử dụng bind mount, Docker sử dụng hệ thống tệp hiện tại trên máy host, cho phép container đọc/ghi trực tiếp vào các tệp đó. Tuy nhiên, bind mount ít linh hoạt hơn so với volume vì nó phụ thuộc vào cấu trúc file hệ thống của host.

  * **Tmpfs mount**: Lưu trữ dữ liệu trong bộ nhớ (RAM) thay vì trên ổ cứng, điều này giúp cải thiện hiệu suất nhưng dữ liệu sẽ bị mất khi container dừng hoạt động.

**Các ưu điểm của Docker Volume:**

  * **Tính bền vững**: Dữ liệu trong volume không bị mất khi container dừng hoặc bị xóa.

  * **Chia sẻ dữ liệu**: Nhiều container có thể chia sẻ một volume để cùng sử dụng chung dữ liệu.

  * **Quản lý dễ dàng**: Docker quản lý volumes độc lập với hệ thống file của container, giúp dễ dàng sao lưu, di chuyển hoặc gắn kết dữ liệu.


## 4. Docker Compose

Docker Compose là một công cụ trong hệ sinh thái Docker, giúp bạn dễ dàng định nghĩa và quản lý nhiều container cùng lúc bằng cách sử dụng tệp cấu hình YAML. Docker Compose cho phép bạn mô tả cách các container của ứng dụng nên hoạt động cùng nhau (chạy đồng thời, chia sẻ mạng, volume, môi trường, v.v.) mà không cần phải khởi chạy từng container thủ công.

Tính năng của Docker Compose:
  
  * **Định nghĩa đa container**: Bạn có thể định nghĩa tất cả các container mà ứng dụng cần trong một file YAML duy nhất. Mỗi container (dịch vụ) được định nghĩa bao gồm image, mạng, volumes, các biến môi trường, và những thông tin cần thiết khác.

  * **Quản lý dễ dàng**: Thay vì khởi chạy từng container một cách riêng lẻ, bạn chỉ cần một lệnh duy nhất để khởi động tất cả các container liên quan. Docker Compose quản lý vòng đời của toàn bộ hệ thống ứng dụng.

  * **Môi trường phát triển**: Docker Compose thường được sử dụng trong phát triển, khi bạn cần chạy toàn bộ hệ thống ứng dụng của mình với tất cả các dịch vụ hỗ trợ (như database, cache, v.v.) một cách dễ dàng.

  * **Khả năng mở rộng**: Bạn có thể mở rộng số lượng các bản sao của container (scale) rất dễ dàng bằng cách thay đổi tệp cấu hình hoặc thông qua các lệnh Docker Compose.

## 5. Docker Swarm

Docker Swarm là một công cụ điều phối container tích hợp sẵn trong Docker, cho phép bạn triển khai và quản lý một cụm (cluster) Docker Engine hoạt động đồng bộ. Docker Swarm giúp quản lý các container chạy trên nhiều máy chủ khác nhau, cung cấp các tính năng như cân bằng tải, tự động phân phối container, và khả năng mở rộng hệ thống một cách linh hoạt.

Tính năng chính của Docker Swarm:

* **Cluster Mode (Chế độ cụm)**: Docker Swarm biến nhiều Docker Engine (máy chủ) thành một cụm hợp nhất. Trong đó, các Docker Engine có thể đảm nhận vai trò quản lý (manager) hoặc worker, và các container sẽ được tự động phân phối giữa các node này.

* **Service và Task**:

   + Service: Được định nghĩa như một thành phần ứng dụng cần chạy. Ví dụ: một service có thể là một container chạy ứng dụng web.
  
  + Task: Là một đơn vị triển khai của service, chạy trên một node trong cụm. Một service có thể mở rộng để tạo ra nhiều task, tương ứng với việc chạy nhiều container song song.

* **Cân bằng tải (Load Balancing)**: Docker Swarm tự động phân phối các container giữa các node trong cụm để cân bằng tải. Nếu một node bị quá tải, Docker Swarm có thể khởi động container trên một node khác.

* **Tự động sửa chữa**: Nếu một node hoặc container bị lỗi, Docker Swarm sẽ tự động khởi động lại container đó trên các node khác, giúp đảm bảo ứng dụng luôn sẵn sàng và hoạt động ổn định.

* **Mở rộng (Scaling)**: Docker Swarm hỗ trợ mở rộng các service rất dễ dàng. Bạn có thể tăng hoặc giảm số lượng container cho một service chỉ với một lệnh duy nhất.

* **Kiến trúc phân tán**: Docker Swarm cho phép bạn triển khai các container trên nhiều máy chủ (node) vật lý hoặc ảo, đảm bảo tính phân tán và khả năng mở rộng của hệ thống.

* **Bảo mật**: Swarm hỗ trợ mã hóa giao tiếp giữa các node và yêu cầu xác thực khi thêm node mới vào cụm. Điều này giúp đảm bảo an toàn cho hệ thống phân tán.


# END