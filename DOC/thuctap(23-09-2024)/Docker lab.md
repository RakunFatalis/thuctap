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
  - [5. Docker Compose](#5-docker-compose)
  - [6. Docker Swarm](#6-docker-swarm)
- [End](#end)



# I. Cài đặt Docker

Trước khi cài đặt Docker Engine lần đầu tiên trên một máy chủ mới, bạn cần thiết lập kho lưu trữ Docker. Sau đó, bạn có thể cài đặt và cập nhật Docker từ kho lưu trữ này.

        # yum install -y yum-utils
        # yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

![](/img/Docker_Yum.png)

![](/img/Docker_Yum_Manager.png)

Để cài đặt Docker ta sử dụng lệnh sau:

        # yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

Lệnh này sẽ cài đăt Docker nhưng chưa kích hoạt hoạt động nó lên. Nó cũng sẽ tạo một group ``docker`` nhưng sẽ không có user nào trong đó.

![](/img/Docker_Install.png)

Sử lệnh sau để kích hoạt docker lên: 

        # systemctl start docker

Xác minh rằng việc cài đặt Docker Engine thành công bằng cách chạy image hello-world.
  
    Lệnh này tải về một image kiểm tra và chạy nó trong một container. Khi container chạy, nó sẽ in ra một thông báo xác nhận và thoát.

        # docker run hello-world

![](/img/Docker_run_hello_world.png)

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

![](/img/Docker_Image.png)

Nếu bạn chỉ muốn hiển thị các mã ID của image, bạn có thể sử dụng cờ ``–quiet``

        # docker image ls -q

**Kéo Docker Images**

Để tải Docker images về máy tính của bạn từ một registry, hãy sử dụng lệnh docker pull. Docker sẽ tự động tải phiên bản 'latest' của image nếu không có tag nào được chỉ định. Trước khi khởi động các container dựa trên các image, lệnh này là cần thiết để lấy các image từ các registry công khai hoặc riêng tư.

        # docker pull ubuntu

![](/img/Docker_Image_pull.png)

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

![](/img/Docker_Image_dockerfile.png)

Bạn sử dụng lệnh sau để tạo một image từ một docker file:

        # docker build -t myapp:latest .

![](/img/Docker_Image_buildimage.png)

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

![](/img/Docker_Container_list.png)

**Chạy Một Docker Container**

Lệnh chính để bắt đầu và tạo các Docker container là ``docker run``. Khi bạn sử dụng lệnh này, Docker sẽ thực hiện các bước sau:

  1. Kiểm Tra Image: Nếu image không có sẵn trên máy tính của bạn, Docker sẽ tự động tải nó từ một registry (ví dụ: Docker Hub).

  2. Tạo Container: Docker sẽ khởi động một instance mới của container dựa trên image đó.

Cúp pháp cơ bản:

    # docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Với lệnh này, bạn có thể chỉ định nhiều tùy chọn khác nhau, bao gồm việc gắn (mount) volumes, biến môi trường (environment variables), ánh xạ cổng (port mappings), và nhiều tùy chọn khác để tùy chỉnh cấu hình của container theo yêu cầu của bạn.

    # docker run busybox        # Cài đặt Container của busy box khi chưa có image.

![](/img/Docker_Container_run.png)

**Dừng Một Docker Container**

Container có thể được dừng một cách an toàn bằng cách sử dụng lệnh ``docker stop``. Lệnh này gửi tín hiệu ``SIGTERM`` đến tiến trình chính của container, cho phép nó thực hiện các thao tác dọn dẹp cần thiết trước khi tắt.

Cú pháp cơ bản

        # docker stop CONTAINER_NAME_OR_ID

![](/img/Docker_Container_stop.png)

**Tạm Dừng Một Docker**

Lệnh ``docker pause`` tạm thời dừng các tiến trình của container mà không dừng hoàn toàn container. Tất cả các tiến trình bên trong container sẽ bị tạm ngưng cho đến khi container được tiếp tục. Lệnh này rất hữu ích khi bạn muốn giải phóng tài nguyên hệ thống mà không cần phải dừng và khởi động lại container.

Cú pháp cơ bản:

        # docker pause CONTAINER_NAME_OR_ID

![](/img/Docker_Container_pause.png)

**Tiếp Tục Chạy Container**

Khi một container đã được tạm dừng, bạn có thể tiếp tục thực hiện các tiến trình bên trong container bằng cách sử dụng lệnh ``docker unpause``. Lệnh này sẽ khôi phục trạng thái ban đầu của container và tiếp tục các tiến trình đã bị tạm dừng bởi lệnh docker pause.

Cú pháp cơ bản:
        # docker unpause CONTAINER_NAME_OR_ID 

**Khởi động lại Container**

Lệnh docker restart cho phép bạn dừng một container đang hoạt động và khởi động lại nó trong một bước đơn giản. Điều này rất hữu ích khi bạn muốn làm mới trạng thái của container hoặc áp dụng các thay đổi cấu hình mà không cần phải dừng và khởi động lại container một cách thủ công.

Cú pháp cơ bản:

        # docker restart CONTAINER_NAME_OR_ID

![](/img/Docker_Container_restart.png)

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

![](/img/Docker_Network_Create.png)

**Liệt Kê Các Mạng Docker**

Để liệt kê tất cả các mạng trên máy chủ của bạn, bạn có thể sử dụng lệnh docker network ls. Lệnh này sẽ hiển thị danh sách tất cả các mạng cùng với tên và driver của chúng.

        # docker network ls

**Kiểm Tra Thông Tin Mạng Docker**

Khi làm việc với các mạng trong Docker, bạn có thể cần lấy thông tin liên quan đến các mạng trên máy chủ của mình. Lệnh ``docker network inspect`` giúp bạn lấy thông tin chi tiết về một mạng cụ thể.

Cú pháp cơ bản:

        # docker network inspect NETWORK_NAME

Khi bạn chạy lệnh này, bạn sẽ nhận được thông tin chi tiết dạng JSON.

![](/img/Docker_Network_Inspect.png)

**Kết Nối Một Container Vào Mạng Docker**

Nếu bạn đã tạo một mạng và muốn kết nối một container đang chạy vào mạng đó, bạn có thể sử dụng lệnh ``docker network connect``. Điều này cho phép container giao tiếp với các container khác trên mạng đã chỉ định trong lệnh.

Cú pháp cơ bản:

        # docker network connect NETWORK_NAME CONTAINER_NAME_OR_ID

![](/img/Docker_Network_Connect.png)

**Ngắt kết nối một container khỏi một mạng**

Nếu một mạng được liên kết với một container và bạn muốn ngắt kết nối nó khỏi container, bạn có thể sử dụng lệnh ``docker network disconnect``. Lệnh này sẽ xóa kết nối của container với mạng được chỉ định.

Cú pháp cơ bản:

        # docker network disconnect NETWORK_NAME CONTAINER_NAME_OR_ID

![](/img/Docker_Network_Disconnect.png)

**Xóa một mạng**

Nếu một mạng không còn cần thiết nữa, bạn có thể xóa nó khỏi hệ thống bằng lệnh ``docker network rm``. Với lệnh này, bạn chỉ có thể xóa những mạng không đang được sử dụng bởi bất kỳ container nào.

Cú pháp cơ bản:

        # docker network rm NETWORK_NAME

![](/img/Docker_Network_Remove.png)

**Xóa các mạng không sử dụng**

Nếu bạn muốn xóa tất cả các mạng Docker không được sử dụng để giải phóng tài nguyên, bạn có thể sử dụng lệnh ``docker network prune``. Trước khi xóa các mạng, lệnh này sẽ yêu cầu bạn xác nhận để đảm bảo chắc chắn.

Cú pháp cơ bản:

        # docker network prune

## 4. Docker Volume

**Tạo một Docker Volume**

Nếu bạn muốn tạo một volume mới trong Docker, bạn có thể sử dụng lệnh ``docker volume create``. Các volume được tạo bằng lệnh này có thể được sử dụng bởi một hoặc nhiều container.

Cú pháp cơ bản:

        #  docker volume create [OPTIONS] VOLUME_NAME

![](/img/Docker_Volume_Create.png)

**Liệt kê Docker Volumes**

Việc liệt kê các volume trong máy chủ cục bộ là một trong những lệnh thường xuyên được sử dụng để giúp bạn quản lý các volume. Nếu bạn muốn liệt kê tất cả các Docker volume trên hệ thống của mình, bạn có thể sử dụng lệnh ``docker volume ls``.

Cú pháp cơ bản:

        # docker volume ls

**Kiểm tra một Docker Volume**

Khi bạn muốn lấy thông tin chi tiết về một volume cụ thể, bạn có thể sử dụng lệnh ``docker volume inspect``. Lệnh này yêu cầu bạn cung cấp tên hoặc ID của volume, thông tin này có thể lấy được bằng lệnh liệt kê volume. Nó sẽ cung cấp các chi tiết như vị trí của volume trên máy chủ và cấu hình của nó.

Cú pháp cơ bản:

        # docker volume inspect VOLUME_NAME

![](/img/Docker_Volume_Inspect.png)

**Xóa một Docker Volume**

Nếu bạn muốn dọn dẹp máy cục bộ và xóa các Docker volume không còn cần thiết, bạn có thể sử dụng lệnh ``docker volume rm``. Lệnh này cho phép bạn xóa những volume không còn được sử dụng bởi bất kỳ container nào.

Cú pháp cơ bản:

        # docker volume rm VOLUME_NAME

**Sử dụng Docker Volume với một Container**

Khi bạn chạy một container, bạn có thể chỉ định volume bằng tùy chọn ``-v`` hoặc ``--mount``. Tùy chọn ``-v`` đơn giản hơn và được sử dụng phổ biến hơn, trong khi ``--mount`` cung cấp nhiều tùy chọn cấu hình nâng cao hơn.

Cách sử dụng -v:

        # docker run -v VOLUME_NAME:/path/in/container IMAGE_NAME

Trong đó:

  + **VOLUME_NAME**: là tên của volume bạn muốn gắn vào container.

  + **/path/in/container**: là đường dẫn trong container nơi volume sẽ được gắn vào.

  + **IMAGE_NAME**: là tên của image mà container sẽ chạy.

![](/img/Docker_Volume_Container_v.png)

Cách sử dụng --mount:

        # docker run --mount type=volume,source=VOLUME_NAME,target=/path/in/container IMAGE_NAME

Trong đó:

  + **type=volume**: Xác định rằng loại mount là volume (bạn cũng có thể sử dụng type=bind để mount một thư mục từ host).

  + **source=VOLUME_NAME**: Tên của volume bạn muốn gắn vào container.

  + **target=/path/in/container**: Đường dẫn trong container nơi volume sẽ được gắn.

  + **IMAGE_NAME**: Tên của image mà container sẽ chạy.

**Xóa các Volume không sử dụng**

Lệnh ``docker volume rm`` chỉ cho phép bạn xóa từng volume một. Nhưng nếu bạn muốn xóa tất cả các volume không còn sử dụng để giải phóng không gian trên máy, bạn có thể sử dụng lệnh ``docker volume prune``. Khi bạn chạy lệnh này, Docker sẽ yêu cầu bạn xác nhận trước khi xóa tất cả các volume không còn được liên kết với container nào (dangling volumes).

Cú pháp cơ bản:

        # docker volume prune

**Sao lưu một Docker Volume**

Việc sao lưu dữ liệu lưu trữ trong các volume là rất hữu ích, vì nếu bạn vô tình xóa volume, bạn có thể phục hồi dữ liệu đã mất. Bạn có thể lưu trữ dữ liệu trong volume vào một tệp tarball. Để làm điều này, bạn có thể sử dụng một container để nén nội dung của volume và xuất nó ra một tệp trên hệ thống máy chủ.

        # docker run --rm -v my_volume:/volume -v $(pwd):/backup ubuntu tar cvf /backup/my_volume_backup.tar /volume

Trong đó:

  + ``docker run``: Khởi động một container mới.

  + ``--rm``: Tự động xóa container sau khi lệnh thực thi xong.

  + ``-v my_volume:/volume``: Gắn volume my_volume vào container tại đường dẫn /volume.

  + ``-v $(pwd):/backup``: Gắn thư mục hiện tại (dùng $(pwd) để lấy đường dẫn đầy đủ) vào container tại đường dẫn /backup. Điều này cho phép bạn lưu tệp sao lưu vào thư mục hiện tại trên máy chủ.

  + ``ubuntu``: Tên image mà bạn đang sử dụng, trong trường hợp này là Ubuntu.

  + ``tar cvf /backup/my_volume_backup.tar /volume``: Lệnh này sẽ nén nội dung trong /volume (nơi chứa dữ liệu của volume) và lưu vào tệp my_volume_backup.tar trong thư mục /backup (trên máy chủ).

**Khôi phục một Docker Volume từ Sao lưu**

Khi bạn đã có dữ liệu được sao lưu trong một tệp tarball, bạn có thể sử dụng lệnh dưới đây để khôi phục nó trở lại một Docker volume. Dưới đây là lệnh ví dụ để khôi phục một volume có tên là my_volume từ tệp sao lưu:

        # docker run --rm -v my_volume:/volume -v $(pwd):/backup ubuntu bash -c "tar xvf /backup/my_volume_backup.tar -C /volume --strip 1"


Giải thích lệnh:

+ ``docker run``: Khởi động một container mới.

+ ``--rm``: Tự động xóa container sau khi lệnh thực thi xong.

+ ``-v my_volume:/volume``: Gắn volume my_volume vào container tại đường dẫn /volume.

+ ``-v $(pwd):/backup``: Gắn thư mục hiện tại (sử dụng $(pwd) để lấy đường dẫn đầy đủ) vào container tại đường dẫn /backup.

+ ``ubuntu``: Tên image mà bạn đang sử dụng, trong trường hợp này là Ubuntu.

+ ``bash -c "tar xvf /backup/my_volume_backup.tar -C /volume --strip 1"``: Lệnh này sẽ giải nén nội dung trong tệp sao lưu my_volume_backup.tar vào /volume. Tùy chọn --strip 1 giúp loại bỏ thư mục gốc trong tệp tarball, do đó chỉ sao chép các tệp và thư mục con trực tiếp vào trong volume.

## 5. Docker Compose

**Cơ chế Tệp Docker Compose (YAML)**

Thông thường, tệp Docker Compose sẽ là tệp ``docker-compose.yml`` sử dụng định dạng YAML. Tệp này mô tả cấu hình mà ứng dụng của bạn cần liên quan đến các dịch vụ, mạng và volume. Nó cung cấp hướng dẫn về cách khởi động môi trường mà ứng dụng sẽ chạy. Việc hiểu cấu trúc của tệp này là rất quan trọng để sử dụng hiệu quả Docker Compose.

Các Yếu Tố Chính của Tệp YAML

  + Version: Xác định định dạng của tệp Docker Compose, đảm bảo tính tương thích với các tính năng khác nhau của Docker Compose.

  + Services: Chứa danh sách tất cả các dịch vụ (container) cấu thành ứng dụng. Mỗi dịch vụ được mô tả với nhiều tùy chọn cấu hình không giới hạn.

  + Networks: Chỉ định các mạng tùy chỉnh cho giao tiếp giữa các container và có thể xác định các tùy chọn cấu hình và driver mạng.

  + Volumes: Khai báo các volume chia sẻ được sử dụng để cho phép lưu trữ bền vững. Các volume có thể được chia sẻ giữa các dịch vụ hoặc được sử dụng để lưu trữ dữ liệu bên ngoài vòng đời của container.

Ví dụ về tệp ``docker-compose.yml``

Dưới đây là một ví dụ cơ bản về tệp docker-compose.yml:

![](/img/Docker_Compose_fileyml.png)



**Lệnh Docker Compose Up**

Lệnh ``docker-compose up`` khởi động và chạy toàn bộ ứng dụng, như được định nghĩa trong tệp d``docker compose.yml``, đồng thời tạo và khởi động tất cả các dịch vụ, mạng và volume. Ngoài ra, nếu hình ảnh (images) của dịch vụ này chưa bao giờ được xây dựng, lệnh sẽ tự động xây dựng các hình ảnh Docker cần thiết.

Cú pháp cơ bản: 

        # docker compose up

![](/img/Docker_Compose_UP.png)

**Lệnh Docker Compose Down**

Lệnh ``docker compose down`` dừng và xóa tất cả các container, mạng và volume được định nghĩa trong tệp ``docker-compose.yml``. Lệnh này giúp bạn dọn dẹp các tài nguyên mà ứng dụng của bạn đã sử dụng cho đến nay, đảm bảo rằng không còn container hoặc mạng nào còn hoạt động ở đâu đó.

Cú pháp cơ bản:

        # docker compose down

![](/img/Docker_Compose_DOWN.png)

``Lệnh Docker Compose Build``

Lệnh ``docker compose build`` được sử dụng để xây dựng hoặc xây dựng lại các hình ảnh Docker cho các dịch vụ được định nghĩa trong tệp docker-compose.yml. Lệnh này sẽ chạy khi có sự thay đổi trong tệp Dockerfile hoặc mã nguồn, nhằm tạo ra các hình ảnh mới.

Cú pháp cơ bản:

        # docker compose build [OPTIONS] [SERVICE...]

**Các Lệnh Docker Compose: Start, Stop, Restart**

Lệnh ``docker compose start``: Bắt đầu các container đã được tạo mà không tái tạo chúng. Lệnh này sẽ khôi phục lại các dịch vụ đã dừng trước đó.

        # docker compose start [SERVICE...]

Lệnh ``docker compose stop``: Dừng các container đang chạy mà không xóa chúng, cho phép bạn khởi động lại các dịch vụ sau này.

        # docker compose stop [SERVICE...]

Lệnh ``docker compose restart``: Hữu ích khi bạn đã thay đổi môi trường hoặc cấu hình và muốn khởi động lại các dịch vụ.

        # docker compose restart [SERVICE...]

**Lệnh Trạng Thái Docker Compose**

Lệnh ``docker compose ps`` hiển thị trạng thái của tất cả các dịch vụ được định nghĩa trong tệp docker-compose.yml, chỉ ra trạng thái của các container, tên của chúng, tình trạng và cổng. Lệnh này được sử dụng để kiểm tra trạng thái hiện tại của các dịch vụ.

        # docker compose ps

## 6. Docker Swarm

**Tạo một người quản lí Swarm**

Chúng ta sẽ phải tạo một manager để xử lý các worker node. Và bạn cũng nên biết rằng manager cũng là một worker node nhưng có một số quyền hạn đặc biệt.

Cú pháp cơ bản: 

        docker swarm init --advertise-addr [Public or Private IP]

![](/img/Docker_Swarm_Create.png)

Nó sẽ tạo ra một dòng lệnh chứa các token id và địa chỉ ip với cổng kết nối. Các bạn hãy lưu lại dòng lệnh này để sau này ta sẽ thêm thành viên vào swarm.

**Thêm Worker Nodes**
Ta thêm worker node của chúng ta vào cụm Swarm bằng cách sử dụng token đã được tạo trước đó.

        # docker swarm join --token <token-id> <ip:port>

Chúng ta sẽ sang máy Worker để sử dụng dòng lệnh này. Lưu ý là bên máy woker cũng phải cài docker thì mới dùng được lệnh này.

![](/img/Docker_Swarm_Join.png)

**Kiểm Tra Các Node**

Bây giờ, hãy kiểm tra trạng thái của cụm Swarm của chúng ta. Thực hiện lệnh dưới đây.

        # docker node ls

![](/img/Docker_Swarm_List.png)

**Tạo Service trong Docker Swarm**

Để tạo một service trong Docker Swarm, bạn có thể sử dụng lệnh ``docker service create``. Một service trong Swarm cho phép bạn triển khai và quản lý các container trên nhiều node trong cụm.

Cú pháp cơ bản:

        # docker service create --name <Name Service> --replicas <number> <image>

![](/img/Docker_Swarm_Service_Create.png)

**Xóa Service trong Docker Swarm**

Để xóa một service trong Docker Swarm, bạn có thể sử dụng lệnh ``docker service rm``. 

        # docker service rm <name service>

**Quản Lý Node trong Docker Swarm**

Trong Docker Swarm, việc quản lý các node là rất quan trọng để duy trì và điều phối hoạt động của cụm. Dưới đây là một số lệnh cơ bản để quản lý các node trong Docker Swarm.

Để kiểm tra trạng thái của tất cả các node trong cụm Swarm, bạn có thể sử dụng lệnh:

        # docker node ls

Nếu bạn muốn xóa một node khỏi cụm, bạn có thể sử dụng lệnh sau trên manager node:

        # docker node rm <name node>

Bạn có thể nâng cấp hoặc hạ cấp một node thành manager hoặc worker. 

Để nâng cấp node thành manager:

        # docker node promote <name node>

Để hạ cấp một node trở thành worker:

        # docker node demote <name node>

Để xem thông tin chi tiết về một node cụ thể

        #docker node inspect <name node>

**Xóa Swarm**

Để xóa một cụm Docker Swarm, bạn cần thực hiện một số bước, tùy thuộc vào việc bạn đang xóa một manager node hay một worker node.

Nếu bạn là một worker node, bạn có thể đơn giản sử dụng lệnh sau để rời khỏi cụm:

        # docker swarm leave

Nếu bạn là một manager node và muốn rời khỏi cụm, bạn có thể sử dụng lệnh:

        # docker swarm leave --force


# End