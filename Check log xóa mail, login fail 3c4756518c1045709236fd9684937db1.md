# Check log xóa mail, login fail

## Cấu hình logs

Trong Kerio Connect administration > Logs.

![Untitled](Check%20log%20xo%CC%81a%20mail,%20login%20fail%203c4756518c1045709236fd9684937db1/Untitled.png)

Khi click chuột phải vào khu vực log, ta có thể thực hiện các thao tác 

### *Save log*

Lưu toàn bộ logs hay từng phần theo định file  `txt` hay `HTML` 

### *Highlighting*

Có thể highlight các phần ghi chú quan trọng để tham khảo. Có thể dùng regex để thực hiện việc tìm kiếm

### *Log Settings*

Cấu hình lưu theo từng log với yêu cầu kích thước và số lượng file

![https://manuals.gfi.com/en/kerio/connect/content/assets/connect-logsettings.png](https://manuals.gfi.com/en/kerio/connect/content/assets/connect-logsettings.png)

## Các dạng logs

### Log cấu hình

Lưu giữ toàn bộ lịch sử việc thay đổi cấu hình và cho biết user name đã thực hiện các tác vụ quản trị khi nào.

### *Debug log*

Giám sát nhiều loại thông tin và dùng để xử lý sự cố

Có thể chọn hiện theo yêu cầu

1. Right-click vào cửa sổ và click **Messages**.
2. Chọn các phần muốn giám sát.
3. Click **OK**.

**LƯU Ý**

Quá nhiều thông có thể gây chậm hiệu suất của Kerio. Sau khi xử lý sự cố hãy xóa các log không cần thiết

### *Mail log*

Chứa thông tin về các tin nhắn cá nhân được xử lý bởi Kerio Connect.

### *Security log*

Chứa thông tin liên quan đến bảo mật, cũng chứa các tin nhắn báo lỗi trong việc gửi nhận

### *Warning log*

Chứa các cảnh báo các sự kiện nhưng không gây ảnh hướng quá đáng kể cho vận hành Kerio Connect nhưng cũng không chủ quan. Nó hỗ trợ đắc lực trong việc các users than phiền về các dịch vụ không hoạt động.

### *Operations log*

Thu thập thông về xóa, di chuyển thư mục, thư tín, liên lạc, sự kiện, tác vụ và ghi chú trong hộp thư, nó đặc biệt hữu ích trong việc user không thể tìm chính xác cụ thể thư tín trong hộp thử của họ

### *Error log*

Chứa các thông tin đáng quan tâm về lỗi nghiêm trọng hoặc đáng kể, thông thường sẽ ảnh hưởng đến vận hành của mail server (ngược lại so với Warning log)

Các lỗi thường xuyên về khởi tạo dịch vụ, thường là xung đột với các cổng dịch vụ, dung lượng lưu trữ, khởi tạo việc phòng ngừa virus, xác thực sai của user …

### *Spam log*

Thể hiện các thông tin về địa chỉ email có dấu hiệu Spam trong Kerio.

### *Audit log*

Chứa đựng các thông tin về xác thực thành công vào tài khoản Kerio, bao gồm Kerio Connect accounts, Kerio Connect Administration, Kerio Connect Client, Microsoft Outlook with KOFF, etc.