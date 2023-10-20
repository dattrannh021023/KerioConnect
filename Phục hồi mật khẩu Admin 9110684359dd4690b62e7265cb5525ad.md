# Phục hồi mật khẩu Admin

1. Dừng Kerio Connect Engine. 

```bash
systemctl stop kerio-connect
```

1. Vào thư mục chứa cài đặt của Kerio tại `opt/kerio/mailserver`

```bash
cd /opt/kerio/mailserver
```

1. Chỉnh file `users.cfg`

```bash
vi users.cfg
```

1. Tìm tên của admin trong thẻ `<variable name="Name">Admin</variable>`
2. Bên dưới tên của Admin có dòng mật khẩu dưới dạng sau `<variable name="Password">`. For example: `<variable name="Password">D3S:22d1da9fa35569fc075aa577936b4be6259caeafe9a42324</variable>`

![Untitled](Phu%CC%A3c%20ho%CC%82%CC%80i%20ma%CC%A3%CC%82t%20kha%CC%82%CC%89u%20Admin%209110684359dd4690b62e7265cb5525ad/Untitled.png)

1. Thay mật khẩu bằng `NUL:`. Ví dụ: `<variable name="Password">NUL:</variable>`
2. Lưu file
3. Khởi động lại Kerio Connect engine.

```bash
systemctl start kerio-connect
```

1. Đăng nhập vào tài khoản admin bằng mật khẩu rỗng.