# REDIRECT

# MỤC LỤC


## Giới thiệu

Chuyển hướng đầu vào và đầu ra (Input and Output Redirection) là một kỹ thuật quan trọng trong hệ điều hành Linux, cho phép người dùng điều khiển luồng dữ liệu giữa các lệnh, tệp và thiết bị đầu vào/đầu ra. Kỹ thuật này giúp tăng cường hiệu suất và tính linh hoạt trong việc sử dụng các lệnh của Linux.

## Overwrite Redirection

Overwrite Redirection (chuyển hướng ghi đè) trong Linux là một kỹ thuật chuyển hướng đầu ra của một lệnh vào một tệp, ghi đè nội dung hiện có của tệp đó. Đây là một cách hiệu quả để lưu trữ kết quả của các lệnh, nhưng nó sẽ xóa bất kỳ nội dung nào đã tồn tại trong tệp trước đó.

### 1. Toán tử >

``>``: Dùng để chuyển hướng đầu ra tiêu chuẩn (stdout) của một lệnh vào một tệp. Nếu tệp đã tồn tại, nội dung của nó sẽ bị ghi đè.

**Cú pháp cơ bản:** ``# comand > file``

**Ví dụ:**

``# echo "Asian and EU" > output.txt``

Lệnh này sẽ ghi dòng chữ "Asian and EU" vào tệp ``output.txt``. Nếu ``output.txt`` đã tồn tại, nội dung hiện có của nó sẽ bị ghi đè bởi "Hello, World!".

![](/thuctap/img/echo_standout.png)

``# cat > output.txt``

Lệnh này sẽ ghi đè vào tệp output.txt. Dữ liệu ghi đè sẽ được nhập từ bàn phím.

![](/thuctap/img/cat_standout.png)

### 2. Toán tử <

``<``: Dùng để chuyển hướng đầu vào tiêu chuẩn (stdin) từ một tệp vào một lệnh.

**Cú pháp cơ bản:** ``# comand < file``

**Ví dụ:**

Lệnh này được sử dụng để đọc nội dung của tệp ``output.txt`` và hiển thị nó ra đầu ra tiêu chuẩn (stdout).

``# cat < output.txt``

![](/thuctap/img/cat_standin.png)

## Append Redirection

Append Redirection (Chuyển hướng nối thêm) trong Linux là một kỹ thuật chuyển hướng đầu ra tiêu chuẩn (stdout) vào một tệp mà không ghi đè nội dung hiện có của tệp đó. Thay vào đó, nội dung mới sẽ được thêm vào cuối tệp.

### 1. Toán tử >>
``>>``: Dùng để chuyển hướng đầu ra tiêu chuẩn (stdout) của một lệnh vào một tệp. Nếu tệp đã tồn tại, nội dung mới sẽ được thêm vào cuối tệp mà không ghi đè.

**Cú pháp cơ bản:** ``# comand >> file``

**Ví dụ:**

Lệnh này sẽ thêm dòng "New line" vào cuối tệp output.txt.

``# echo "New Line" > output.txt``

![](/thuctap/img/echo_standin2.png)

### 2. Toán tử <<

``<<``: được sử dụng để định nghĩa và sử dụng ``here document``. ``Here document`` là một cách để cung cấp đầu vào đa dòng cho một lệnh mà không cần phải sử dụng một tệp văn bản riêng biệt

**Cú pháp cơ bản:** ``# command << Marker``

**Ví dụ:**

``# cat << output.txt``

Trong lệnh này:

``<< output.txt`` định nghĩa here document bắt đầu từ dòng tiếp theo và kết thúc khi gặp dòng có từ ``output.txt``.

Các dòng văn bản nằm giữa hai dòng ``output.txt`` sẽ là nội dung được đưa vào lệnh cat.

![](/thuctap/img/cat_output.png)

## Merge Redirection

Merge Redirection trong Linux cho phép bạn điều hướng đầu ra của một lệnh hoặc chương trình vào một file descriptor cụ thể thay vì đầu ra chuẩn.

``p >& q``: Hợp nhất đầu ra từ luồng p với luồng q.

``p <& q``: Hợp nhất đầu vào từ luồng p với luồng q

### 1. Toán tử >&

Toán tử ``>&`` được sử dụng để chuyển hướng đầu ra của một lệnh hoặc chương trình vào một file descriptor (luồng) cụ thể thay vì đầu ra chuẩn (stdout).

**Cú pháp cơ bản:** ``# command >& stream``

Trong đó:

* ``command`` là lệnh hoặc chương trình mà bạn muốn chuyển hướng đầu ra.

* ``stream`` là số thứ tự của file descriptor mà bạn muốn chuyển hướng đầu ra đến.

**Ví dụ:**

``# ls -l >& 2``

Trong lệnh này:

* ``ls -l`` là lệnh để liệt kê các tệp trong định dạng dài.

* ``>& 2`` chuyển hướng đầu ra của ls -l vào file descriptor 2, thường là stderr. Điều này có nghĩa là cả stdout và stderr sẽ được chuyển hướng vào stderr.

    ![](/thuctap/img/ls_stderr.png)

### 2. Toán tử <&

Toán tử ``<&`` cho phép bạn chuyển hướng đầu vào từ một luồng cụ thể (thường là một tệp hoặc một luồng khác) vào lệnh hoặc chương trình thay vì sử dụng đầu vào chuẩn (stdin).

**Cú pháp cơ bản:** ``# command <& stream``

## Error Redirection

"Error redirection" là kỹ thuật cho phép bạn điều hướng đầu ra của lệnh hoặc thông điệp lỗi (error message) sang các vị trí khác nhau thay vì hiển thị trực tiếp trên màn hình hoặc gửi đến standard output (stdout).

Khi bạn chạy một chương trình trong terminal của Unix/Linux, có ba luồng tiêu chuẩn mặc định được tạo ra:

* **Standard Input (0):** Đây là luồng dữ liệu mà chương trình có thể đọc từ đầu vào. Thông thường, nó liên kết với bàn phím để nhận dữ liệu từ người dùng hoặc từ một luồng dữ liệu khác.

* **Standard Output (1):** Đây là luồng dữ liệu mà chương trình ghi đầu ra. Mặc định, đầu ra này sẽ hiển thị trên màn hình terminal nếu không có sự can thiệp.

* **Standard Error (2):** Đây là luồng dữ liệu mà chương trình sử dụng để ghi các thông báo lỗi hoặc thông tin gỡ lỗi. Thông thường, lỗi này sẽ hiển thị trên màn hình terminal như standard output.

**Ví dụ:**

File descriptor sử dụng là 2 (STDERR). Bằng cách sử dụng "``2>``", chúng ta điều hướng đầu ra lỗi sang một tệp tin có tên là "error.txt" và không có gì được hiển thị trên STDOUT (standard output).

``# somerandomcommand 2>error.txt``

![](/thuctap/img/somerandom.png)

lệnh ``ls admin > error.txt 2>&1`` được sử dụng để thực hiện việc:

* Liệt kê các tập tin và thư mục trong thư mục admin.

* Ghi cả đầu ra thông thường và thông báo lỗi (nếu có) vào tệp tin error.txt.

![](/thuctap/img/admin_to_error.png)



# END.
