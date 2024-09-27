# Docker Lab

# Mục lục

- [Docker Lab](#docker-lab)
- [Mục lục](#mục-lục)
- [I. Cài đặt Docker](#i-cài-đặt-docker)
- [II. Làm quen với các hệ sinh thái trong docker](#ii-làm-quen-với-các-hệ-sinh-thái-trong-docker)
  - [1. Docker Image](#1-docker-image)
  - [2. Docker Container](#2-docker-container)
  - [3. Docker Networking](#3-docker-networking)
  - [4. Docker Volume](#4-docker-volume)
- [End](#end)



# I. Cài đặt Docker

Trước khi cài đặt Docker Engine lần đầu tiên trên một máy chủ mới, bạn cần thiết lập kho lưu trữ Docker. Sau đó, bạn có thể cài đặt và cập nhật Docker từ kho lưu trữ này.

        # yum install -y yum-utils
        # yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

![](/thuctap/img/Docker_Yum.png)

![](/thuctap/img/Docker_Yum_Manager.png)

Để cài đặt Docker ta sử dụng lệnh sau:

        # yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

Lệnh này sẽ cài đăt Docker nhưng chưa kích hoạt hoạt động nó lên. Nó cũng sẽ tạo một group ``docker`` nhưng sẽ không có user nào trong đó.

![](/thuctap/img/Docker_Install.png)

Sử lệnh sau để kích hoạt docker lên: 

        # systemctl start docker

Xác minh rằng việc cài đặt Docker Engine thành công bằng cách chạy image hello-world.
  
    Lệnh này tải về một image kiểm tra và chạy nó trong một container. Khi container chạy, nó sẽ in ra một thông báo xác nhận và thoát.

        # docker run hello-world

![](/thuctap/img/Docker_run_hello_world.png)

# II. Làm quen với các hệ sinh thái trong docker

## 1. Docker Image

**Liệt kê Tất cả Docker Images**

Để xem danh sách tất cả các image Docker có trên máy tính của bạn, bạn có thể sử dụng lệnh ``docker images``. Lệnh này cung cấp thông tin quan trọng như kích thước, thời gian tạo, mã ID, tag và tên kho lưu trữ. Sử dụng lệnh này, bạn có thể nhanh chóng xem những image nào có sẵn để chạy các container trên hệ thống của bạn.

Khi bạn chạy lệnh này, bạn sẽ thấy một bảng thông tin với các cột sau:

* **REPOSITORY**: Tên của kho lưu trữ chứa image.
* **TAG**: Thẻ (tag) của image, thường dùng để xác định phiên bản.
* **IMAGE ID**: Mã ID duy nhất của image.
* **CREATED**: Thời gian mà image được tạo.
* **SIZE**: Kích thước của image.

        # docker images

![](/thuctap/img/Docker_Image.png)

Nếu bạn chỉ muốn hiển thị các mã ID của image, bạn có thể sử dụng cờ ``–quiet``

        # docker image ls -q

**Kéo Docker Images**

Để tải Docker images về máy tính của bạn từ một registry, hãy sử dụng lệnh docker pull. Docker sẽ tự động tải phiên bản 'latest' của image nếu không có tag nào được chỉ định. Trước khi khởi động các container dựa trên các image, lệnh này là cần thiết để lấy các image từ các registry công khai hoặc riêng tư.

        # docker pull ubuntu

![](/thuctap/img/Docker_Image_pull.png)

**Xây Dựng Docker Images từ Dockerfile**

Dockerfile là một tệp văn bản chứa tất cả các lệnh cần thiết để xây dựng một Docker image. Bạn có thể tùy chỉnh các image của mình bằng cách định nghĩa các bước trong Dockerfile.

Ta tạo một tệp có tên ``Dockerfile`` trong thư mục của bạn.

Trong tệp Dockerfile ta thêm nội dung này vào:

        # Sử dụng image cơ sở từ Docker Hub
        FROM alpine:3.14

        # Đặt thư mục làm việc bên trong container
        WORKDIR /app

        # Sao chép các tệp ứng dụng từ máy chủ vào container
        COPY . .

        # Expose một cổng cho ứng dụng (tùy chọn)
        EXPOSE 8080

        # Định nghĩa lệnh để chạy khi container khởi động
        CMD ["./myapp"]

![](/thuctap/img/Docker_Image_dockerfile.png)

Bạn sử dụng lệnh sau để tạo một image từ một docker file:

        # docker build -t myapp:latest .

![](/thuctap/img/Docker_Image_buildimage.png)

**Gán Tag cho Docker Images**

Lệnh ``docker tag`` tạo một tag mới cho một Docker image hiện có. Các tag cho phép bạn gán nhãn và tham chiếu đến nhiều phiên bản của một image. Lệnh này thường được sử dụng trước khi tải một image lên một registry với một tag khác.

        # docker tag myapp:latest myrepo/myapp:v1.0

**Đưa Docker Images lên Registry**

Lệnh ``docker push`` chuyển một Docker image từ máy tính địa phương của bạn lên một registry, chẳng hạn như Docker Hub hoặc một registry riêng tư. Trước khi đẩy một image, hãy đảm bảo rằng bạn đã đăng nhập vào registry bằng lệnh ``docker login``.

        # docker push myrepo/myapp:v1.0

**Xóa Docker Images**

Lệnh ``docker rmi`` xóa một hoặc nhiều Docker images khỏi máy tính địa phương của bạn. Bạn có thể cung cấp tên image hoặc mã ID của image. Lệnh này xóa các images và các tag liên quan của chúng một cách vĩnh viễn, vì vậy hãy sử dụng nó một cách cẩn thận

        # docker rmi myapp:latest

## 2. Docker Container

**Liệt Kê Tất Cả Các Docker Containers**

Để liệt kê tất cả các Docker containers đang chạy trên máy chủ Docker, bạn có thể sử dụng lệnh ``docker ps``. Bạn có thể sử dụng tùy chọn ``-a`` hoặc ``--all`` để hiển thị tất cả các container, bao gồm cả những container đã dừng, vì lệnh docker ps chỉ hiển thị các container đang chạy theo mặc định.

        # docker ps

![](/thuctap/img/Docker_Container_list.png)

**Chạy Một Docker Container**

Lệnh chính để bắt đầu và tạo các Docker container là ``docker run``. Khi bạn sử dụng lệnh này, Docker sẽ thực hiện các bước sau:

  1. Kiểm Tra Image: Nếu image không có sẵn trên máy tính của bạn, Docker sẽ tự động tải nó từ một registry (ví dụ: Docker Hub).

  2. Tạo Container: Docker sẽ khởi động một instance mới của container dựa trên image đó.

Cúp pháp cơ bản:

    # docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Với lệnh này, bạn có thể chỉ định nhiều tùy chọn khác nhau, bao gồm việc gắn (mount) volumes, biến môi trường (environment variables), ánh xạ cổng (port mappings), và nhiều tùy chọn khác để tùy chỉnh cấu hình của container theo yêu cầu của bạn.

    # docker run busybox        # Cài đặt Container của busy box khi chưa có image.

![](/thuctap/img/Docker_Container_run.png)

**Dừng Một Docker Container**

Container có thể được dừng một cách an toàn bằng cách sử dụng lệnh ``docker stop``. Lệnh này gửi tín hiệu ``SIGTERM`` đến tiến trình chính của container, cho phép nó thực hiện các thao tác dọn dẹp cần thiết trước khi tắt.

Cú pháp cơ bản

        # docker stop CONTAINER_NAME_OR_ID

![](/thuctap/img/Docker_Container_stop.png)

**Tạm Dừng Một Docker**

Lệnh ``docker pause`` tạm thời dừng các tiến trình của container mà không dừng hoàn toàn container. Tất cả các tiến trình bên trong container sẽ bị tạm ngưng cho đến khi container được tiếp tục. Lệnh này rất hữu ích khi bạn muốn giải phóng tài nguyên hệ thống mà không cần phải dừng và khởi động lại container.

Cú pháp cơ bản:

        # docker pause CONTAINER_NAME_OR_ID

![](/thuctap/img/Docker_Container_pause.png)

**Tiếp Tục Chạy Container**

Khi một container đã được tạm dừng, bạn có thể tiếp tục thực hiện các tiến trình bên trong container bằng cách sử dụng lệnh ``docker unpause``. Lệnh này sẽ khôi phục trạng thái ban đầu của container và tiếp tục các tiến trình đã bị tạm dừng bởi lệnh docker pause.

Cú pháp cơ bản:
        # docker unpause CONTAINER_NAME_OR_ID 

**Khởi động lại Container**

Lệnh docker restart cho phép bạn dừng một container đang hoạt động và khởi động lại nó trong một bước đơn giản. Điều này rất hữu ích khi bạn muốn làm mới trạng thái của container hoặc áp dụng các thay đổi cấu hình mà không cần phải dừng và khởi động lại container một cách thủ công.

Cú pháp cơ bản:

        # docker restart CONTAINER_NAME_OR_ID

![](/thuctap/img/Docker_Container_restart.png)

**Thực Thi Lệnh Trong Một Container Docker Đang Chạy**

Lệnh docker exec cho phép bạn chạy các lệnh hoặc chương trình bên trong một container đang hoạt động. Điều này rất hữu ích khi bạn cần thực hiện các tác vụ như kiểm tra trạng thái của container, sửa lỗi, hoặc thực hiện các thao tác cụ thể mà không cần phải dừng container.

Cú pháp cơ bản:

        # docker exec [OPTIONS] CONTAINER_NAME_OR_ID <command>

**Xóa Một Container Docker**

Để xóa một hoặc nhiều container Docker, bạn có thể sử dụng lệnh ``docker rm``. Bạn có thể chỉ định ID hoặc tên của container mà bạn muốn xóa. Lệnh này chỉ xóa các container đã dừng mặc định; để xóa force một container đang chạy, bạn có thể sử dụng tag ``-f`` hoặc ``--force``.

Cú pháp cơ bản:

        # docker rm CONTAINER_NAME_OR_ID

## 3. Docker Networking

Docker cung cấp một cơ chế mạng mạnh mẽ giúp các container giao tiếp với nhau và với thế giới bên ngoài. Các mạng Docker cho phép bạn tạo và quản lý các kết nối giữa các container, đồng thời đảm bảo tính bảo mật và hiệu suất.

**Tạo Mạng Docker**

Để tạo một mạng Docker, bạn có thể sử dụng lệnh docker network create. Lệnh này cho phép bạn chỉ định driver và các tùy chọn cho mạng.

Cú pháp cơ bản:

        # docker network create [OPTIONS] NETWORK_NAME

![](/thuctap/img/Docker_Network_Create.png)

**Liệt Kê Các Mạng Docker**

Để liệt kê tất cả các mạng trên máy chủ của bạn, bạn có thể sử dụng lệnh docker network ls. Lệnh này sẽ hiển thị danh sách tất cả các mạng cùng với tên và driver của chúng.

        # docker network ls

**Kiểm Tra Thông Tin Mạng Docker**

Khi làm việc với các mạng trong Docker, bạn có thể cần lấy thông tin liên quan đến các mạng trên máy chủ của mình. Lệnh ``docker network inspect`` giúp bạn lấy thông tin chi tiết về một mạng cụ thể.

Cú pháp cơ bản:

        # docker network inspect NETWORK_NAME

Khi bạn chạy lệnh này, bạn sẽ nhận được thông tin chi tiết dạng JSON.

![](/thuctap/img/Docker_Network_Inspect.png)

**Kết Nối Một Container Vào Mạng Docker**

Nếu bạn đã tạo một mạng và muốn kết nối một container đang chạy vào mạng đó, bạn có thể sử dụng lệnh ``docker network connect``. Điều này cho phép container giao tiếp với các container khác trên mạng đã chỉ định trong lệnh.

Cú pháp cơ bản:

        # docker network connect NETWORK_NAME CONTAINER_NAME_OR_ID

![](/thuctap/img/Docker_Network_Connect.png)

**Ngắt kết nối một container khỏi một mạng**

Nếu một mạng được liên kết với một container và bạn muốn ngắt kết nối nó khỏi container, bạn có thể sử dụng lệnh ``docker network disconnect``. Lệnh này sẽ xóa kết nối của container với mạng được chỉ định.

Cú pháp cơ bản:

        # docker network disconnect NETWORK_NAME CONTAINER_NAME_OR_ID

![](/thuctap/img/Docker_Network_Disconnect.png)

**Xóa một mạng**

Nếu một mạng không còn cần thiết nữa, bạn có thể xóa nó khỏi hệ thống bằng lệnh ``docker network rm``. Với lệnh này, bạn chỉ có thể xóa những mạng không đang được sử dụng bởi bất kỳ container nào.

Cú pháp cơ bản:

        # docker network rm NETWORK_NAME

![](/thuctap/img/Docker_Network_Remove.png)

**Xóa các mạng không sử dụng**

Nếu bạn muốn xóa tất cả các mạng Docker không được sử dụng để giải phóng tài nguyên, bạn có thể sử dụng lệnh ``docker network prune``. Trước khi xóa các mạng, lệnh này sẽ yêu cầu bạn xác nhận để đảm bảo chắc chắn.

Cú pháp cơ bản:

        # docker network prune

## 4. Docker Volume
# End