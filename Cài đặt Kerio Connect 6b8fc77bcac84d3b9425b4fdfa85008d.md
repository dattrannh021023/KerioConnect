# Cài đặt Kerio Connect

Chuẩn bị một VPS chạy hệ điều hành `CentOS 7.` 

Tải về phiên bản mới nhất của Kerio Connect cho hệ thống bằng file RPM bằng cách sử dụng công cụ WGET để tải về.

Ở đây ta sử dụng phiên bản 9.2. Dùng lệnh wget để download file `kerio-connect-9.2.10-4692-linux-x86_64.rpm`

```bash
wget -O kerio-connect-9.2.10-4692-linux-x86_64.rpm http://cdn.kerio.com/dwn/connect/connect-9.2.10-4692/kerio-connect-9.2.10-4692-linux-x86_64.rpm
```

Trước khi tiến hành cài đặt, dùng lệnh kiểm tra dịch vụ Mail Server `Postfix` có đang chạy nền hay không

```bash
systemctl status postfix
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled.png)

Nếu chạy thì `stop` dịch vụ và không cho tự khởi động khi startup bằng lệnh `disable`

```bash
systemctl disable postfix
systemctl stop postfix
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%201.png)

Cài đặt `Kerio Connect` bằng lệnh sau

```bash
yum -y install kerio-connect-9.2.10-4692-linux-x86_64.rpm
```

Sau khi quá trình cài đặt hoàn tất sẽ có giao diện sau

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%202.png)

Tiến hành kiểm tra dịch vụ `kerio-connect` đã chạy chưa

```bash
systemctl status kerio-connect
```

Cấu hình tường lửa để cho phép quản trị từ xa (thông qua cổng 4040) và các giao thức của Kerio Connect:

```bash
firewall-cmd --get-active-zones
firewall-cmd --zone=public --add-port=4040/tcp --permanent
```

Reload lại tường lửa

```bash
firewall-cmd --reload
```

Vào URL [https://103.159.50.156:4040/admin](https://103.159.50.156:4040/admin) . Một cảnh báo rủi ro về an toàn thông tin trên website vì thiếu certificate SSL. Cảnh báo như sau: Your connection is not private, click the Advanced button and proceed to the link.

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%203.png)

Sau khi cài đặt thành công, ta vào phần quản trị để cấu hình `SPF`, `DKIM`, `DMARC` trên DNS [tueminh.cc](http://tueminh.cc) để tăng cường bảo mật và độ tin cậy cho hệ thống email, các cơ chế này hoạt động cùng nhau để đảm bảo rằng email gửi từ tên miền tueminh.cc là hợp pháp và không bị giả mạo, phòng tránh email spam trong hệ thống email

Phần domain ta Rename thành tueminh.cc

Sau đó click vào checkbox `Sign outgoing messages from this domain with DKIM signature`**.**, click vào nút `Show public key` để lấy thông tin đưa vào DNS

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%204.png)

`DKIM` có dạng như sau

```bash
DKIM
Loại: TXT
Tên: mail._domainkey
Giá trị: v=DKIM1;p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAy9LIjABQ4p1sNdvzhWDSw4lzbq
q27ud//ouUMphC5eAG5GfM3JreVfDNAU6ApiXEFQsuepyHsOQ4kTQqPm4Gqpf/deYYgtJf7ykyrWllBM
a8qIlTi+rw121yEXmFshnq4bl+/+leV84J+//VQsGYEJ/F4rBNnbASLnU0kZ6mRnLctKBFea/xFFKAMe
UK1zi7wk3zZIkYck/7Wd5flmnI0rDdvZdbV0SqLl5zLR/eMdyTGGAgVZebxkZHuRbNZipiiZe5Ec8llu
TlVdoJECTsqT6MFXsmVlc4zgNttY2vD+TF11D+d/WbH9Ay4PT9hyeemOmxlrVIXhhwoaA/zo9fPwIDAQ
AB
TTL:3600
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%205.png)

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%206.png)

Tiếp tục add `DMARC` vào DNS

```bash
DMARC
Loại: TXT
Tên: _dmarc
Giá trị: v=DMARC1;p=none;pct=100;rua=mailto:admin@tueminh.cc
TTL:3600
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%207.png)

Và cuối cùng add `SPF`

```bash
SPF
Loại: TXT
Tên: ""
Giá trị: v=spf1 ip4:103.159.50.156 -all
TTL:3600
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%208.png)

Tiến hành phân giải ngược địa chỉ IP sang domain

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%209.png)

Sau đó thêm một số trường thông tin vào DNS như

Phân giải domain sang IP

```bash
Loại: A
Tên: mail
Giá trị: 103.159.50.156
TTL:3600
```

```bash
Loại: MX
Tên: ""
Giá trị: mail.tueminh.cc
TTL:3600
```

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%2010.png)

Tạo `MX` chuyển đến domain mail server

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%2011.png)

Sau đó tiến hành tạo 2 tài khoản `dattran@tueminh.cc` và `syha@tueminh.cc`, tiến hành gửi mail qua lại. Đồng thời áp dụng chức năng `Message Filter` để chuyển tự động các email có subject có chứa từ “visa” vào email của `admin@tueminh.cc`

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%2012.png)

![Untitled](Ca%CC%80i%20%C4%91a%CC%A3%CC%86t%20Kerio%20Connect%206b8fc77bcac84d3b9425b4fdfa85008d/Untitled%2013.png)

test forward mail (giữ 1 bản và chuyển đi xóa mail ở mail cũ luôn)
kiểm tra queue mail
xóa mail (giữ lại folder data và xóa luôn folder data)

Thêm đuôi file đính kèm (Configuration > Attachment filter)
Check log xóa mail, login fail