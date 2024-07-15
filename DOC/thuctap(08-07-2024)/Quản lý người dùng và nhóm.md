# QUẢN LÝ NGƯỜI DÙNG VÀ NHÓM

# MỤC LỤC


- [QUẢN LÝ NGƯỜI DÙNG VÀ NHÓM](#quản-lý-người-dùng-và-nhóm)
- [MỤC LỤC](#mục-lục)
  - [I. Tạo và quản lý người dùng](#i-tạo-và-quản-lý-người-dùng)
    - [1. Tạo người dùng mới](#1-tạo-người-dùng-mới)
    - [2. Quản lí mật khẩu và thông tin người dùng](#2-quản-lí-mật-khẩu-và-thông-tin-người-dùng)
  - [II. Quản lí nhóm](#ii-quản-lí-nhóm)
    - [1. Tạo và quản lý nhóm](#1-tạo-và-quản-lý-nhóm)
    - [2. Cấp quyền sudo](#2-cấp-quyền-sudo)
- [END](#end)


## I. Tạo và quản lý người dùng
### 1. Tạo người dùng mới

* Để có thể tạo được tài khoản trong Linux nhất thiết bạn phải đăng nhập bằng tài khoản root. Xét riêng trường hợp tạo tài khoản trong Linux bằng câu lệnh có 2 cách được sử dụng: ``useradd`` và ``adduser``.
    
    **Cấu trúc câu lệnh:** 
    
    ``# useradd [Option] <Tên tài khoản>`` 
    
    ``# adduser <Tên tài khoản>``

    **Trong đó:**
    
    | Option | Mô tả |
    |----------|-------|
    | `-p` | Nhập mật khẩu cho tài khoản |
    | `-c` | Thêm thông tin cho tài khoản |
    | `-d` | Chỉ đường dẫn chưa thư mục home của tài khoản |
    | `-g` | Chỉ ra nhóm tài khoản muốn thuộc |
    | `-s` | Xác định shell cho hệ thống |
    | `-u` | Xác định chỉ số UID của người dùng |
    | `-e` | Xác định thời gian hết hạn của tài khoản |
    | `-f` | Xác định số ngày password sẽ vô hiệu hóa khi tài khoản hết hạn |

    Ví dụ:
    
    ``# useradd new_user1``

    ``# adduser new_user2``

   **Sự khác nhau giữa 2 câu lệnh**

   Câu lệnh ``useradd`` sử dụng tất cả các thông số mà khi người root nhập vào để tạo tài khoản. Còn đối với cách tạo sử dụng câu lệnh ``adduser`` hệ thống sẽ tương tác trực tiếp với người tạo để đưa ra các câu hỏi. Qua đó giúp người sử dụng dễ dàng tạo hơn.

   **Hình ảnh minh hoạ cho adduser**

   ![](/img/adduser.png)

### 2. Quản lí mật khẩu và thông tin người dùng

* Để có thể thêm mật khẩu cho người dùng trên Linux ta nhập cú pháp câu lệnh như sau:

    ``# passwd [options] [username]``

    **Trong đó:**

    | Option | Mô tả |
    |----------|-------|
    | `-l` | Khóa tài khoản người dùng |
    | `-u` | Mở khóa tài khoản người dùng |
    | `-d` | Xóa mật khẩu của người dùng |
    | `-S` | Hiển thị trạng thái của mật khẩu người dùng |
    | `-e` | Hết hạn mật khẩu của người dùng |
    | `-i` | Đặt số ngày không hoạt động cho mật khẩu của người dùng |

    ``username`` (tuỳ chọn): Tên người dùng mà bạn muốn thay đổi mật khẩu. Nếu không cung cấp, mật khẩu của người dùng hiện tại sẽ được thay đổi.
    
    **Ví dụ:**
    
    ![](/img/passwd_user.png)

* Để quản lí thông tin người dùng ta sử dụng câu lệnh ``usermod``, cú pháp câu lệnh như sau:

    ``# usermod [options] [username]``

    **Trong đó:**

    | Option | Mô tả |
    |----------|-------|
    | ``-a``| Thêm user vào một nhóm. Chỉ sử dụng khi đi kèm với lựa chọn ``-G`` |
    | ``-c``| Thêm hoặc sửa đổi thông tin mô tả cho người dùng |
    | ``-d``| Chỉ định thư mục home mới cho người dùng |
    | ``-g``| Chỉ định nhóm chính mới cho người dùng |
    | ``-s``| Chỉ định shell mặc định mới cho người dùng |
    | ``-u``|Chỉ định ID người dùng mới (UID) |
    | ``-e``| Chỉ định ngày hết hạn của tài khoản (dạng YYYY-MM-DD) |

    ``username``: Tên người dùng mà bạn muốn sửa đổi các thuộc tính.

    **Ví dụ:** Thay đổi ngày hết hạn của tài khoản

    ![](/img/datechange.png)

## II. Quản lí nhóm
### 1. Tạo và quản lý nhóm

  * **Tạo một nhóm**

    Chúng ta sử dụng lệnh ``groupadd`` để tạo một nhóm trên hệ thống, cú pháp câu lệnh như sau:

    ``# groupadd [options] group_name``

    **Các option:**
    | Option | Mô tả |
    |----------|-------|
    | ``-f``| Sử dụng khi nhóm đã tồn tại, để buộc ghi đè lên các thay đổi. |
    | ``-h``| Hiển thị trợ giúp về việc sử dụng và thoát. |
    | ``-v``| In ra phiên bản của `groupadd` và thoát. |
    | ``-g``| Chỉ định ID nhóm cho nhóm mới được tạo.|
    | ``-K``| Thiết lập một thuộc tính cho nhóm|
    | ``-o``| Cho phép tạo một nhóm với GID không duy nhất. |
    | ``-p``|Chỉ định mật khẩu cho nhóm.|
    | ``-r``| Tạo một nhóm hệ thống với GID nhỏ hơn 1000. |
    | ``-R``| Áp dụng thay đổi trong thư mục chroot. |
    | ``-Z``| Thiết lập bối cảnh bảo mật SELinux của nhóm mới. |

    **Ví dụ:**
    Nếu chúng ta muốn tạo một nhóm tên là "ketoan", chúng ta sử dụng câu lệnh như sau:

    ``# groupadd ketoan``

    Chúng ta muốn kiểm tra các group mới được tạo, ta sử dụng câu lệnh ``tail`` để kiểm tra, thông thường các group được tạo nằm trong đường dẫn thư mục ***/etc/group*** :

    ``# tail /etc/group``

    ![](/img/tailgroup.png)

    Nó sẽ hiện ra các thông tin của group theo form sau:

    ***group_name*** *:* ***password*** *:* ***group-id*** *:* ***list-of-members***

  * **Thay đổi thuộc tính của nhóm**

    Chúng ta sử dụng lệnh ``groupmod`` để thay đổi các thuộc tính của nhóm, cú pháp câu lệnh như sau:

    ``# groupmod [options] group_name``

    **Các option**
    | Option | Mô tả |
    |----------|-------|
    | ``-g``| Chỉ định Group ID (GID) mới cho nhóm. |
    | ``-h``| Hiển thị trợ giúp về việc sử dụng và thoát. |
    | ``-n``| Đổi tên của nhóm. |
    | ``-o``| Cho phép sử dụng một GID không duy nhất.|
    | ``-p``| Thay đổi mật khẩu của nhóm|
    | ``-o``| Cho phép tạo một nhóm với GID không duy nhất. |
    | ``-R``| Thực hiện thay đổi trong thư mục chroot|

    **Ví dụ:**
    Nếu chúng ta muốn thay đổi một nhóm tên là "ketoan" sang ""kythuat, chúng ta sử dụng câu lệnh như sau:

    ``# groupmod -n kythuat ketoan``

    ![](/img/group_n.png)

    Như thế chúng ta đổi tên nhóm của "ketoan" thành "kythuat".

  * **Xoá một nhóm**

    Để xoá một nhóm ta sử dụng lệnh `groupdel`, cú pháp câu lệnh như sau:

    ``# groupdel [options] group_name``

    **Ví dụ:**

    Giả sử chúng ta muốn xoá nhóm "kythuat", ta sử dụng câu lệnh như sau:

    ``# groupdel kythuat``
  
  * **Thêm người dùng vào nhóm**

    Để thêm người dùng vào nhóm, ta sử dụng câu lệnh ``usermod -a -G``, cú pháp câu lệnh như sau:

    ``# usermod -a -G [group_name] [user_name]``

    **Ví dụ:**
    Nếu chúng ta muốn thêm ``new_user1`` vào nhóm ``ketoan``

    ``# usermod -a -G ketoan new_user1``

    ![](/img/usermod-a-g.png)


> [!WARNING]
> Lưu ý rằng hãy luôn sử dụng tùy chọn **-a (append)** khi thêm người dùng vào một nhóm mới, nếu không thì người dùng sẽ bị xóa khỏi các nhóm không được liệt kê sau tùy chọn **-G** (tức là sẽ xóa user ra khỏi các nhóm khác).
>
>Nếu người dùng hoặc nhóm không tồn tại trên hệ thống thì lệnh usermod sẽ hiển thị một cảnh báo.




### 2. Cấp quyền sudo

  * **Bước 1:** Truy cập vào quyền root của máy chủ

    Dùng câu lệnh:  ``sudo -i``

    Máy chủ sẽ yêu cầu tài khoản root và mật khẩu root của bạn.

* **Bước 2:** Tạo user và password mới

    Dùng câu lệnh ``useradd`` để tạo user mới
    
    Dùng câu lệnh ``passwd`` để đặt mật khẩu cho user

    ![](//img/step2_sudo.png)

* **Bước 3:** Cấp quyền cho User

    Để cấp quyền cho User mới, sử dụng câu lệnh ``usermod`` để thêm User vào nhóm sudo.

    Nhóm sudo là nhóm mặc định có quyền sudo của máy chủ

    ``# usermod -a -G sudo admin_1``

    Dùng câu lệnh để truy cập vào tài khoản "admin_1" 

    ``# su - admin_1``

    Dùng lệnh ``# sudo df -h`` để kiểm tra dung lượng cho máy chủ bằng quyền root từ user **"admin_1"**

    ![](//img/su_admin_1.png)

    Như vậy chúng ta đã cấp được quyền sudo cho user.

    Trường hợp chúng ta muốn thu hồi quyền sudo của user lại thì sao.

    Ta sử dụng câu lệnh ``deluser`` để xoá bỏ quyền sudo

    ``# deluser admin_1 sudo``

    ![](/img/removesudo.png)

# END
