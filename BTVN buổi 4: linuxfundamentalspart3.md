link bài tập: https://tryhackme.com/room/linuxfundamentalspart3<br>
*. task 3<br>
- vim tiên tiến hơn nano<br>

1. Edit "task3" located in "tryhackme"'s home directory using Nano. What is the flag?<br>
- 'nano task3'<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/ab1a70b8-b9f3-4acf-b35a-d683c13684a6)<br>

As: THM{TEXT_EDITORS}<br>

*. task 4<br>
- scp: truyền tệp giữa 2 máy tính = ssh để cung cấp cả xác thực và mã hóa
- chạy 'python3 -m http.server' để khởi động module -> biến máy tính của bn thành 1 máy chủ web để phục vụ các tệp của riêng mk. sau đó xài wget để tải tệp<br>
1. sao chép tệp từ máy mk sang mt từ xa<br>
- 'scp [tên tệp trên máy mk] [tên ng dùng trên mt từ xa]@[IP của mt từ xa]:/home/[tên ng dùng trên mt từ xa]/[tên tệp trên mt từ xa]'<br>

2. sao chép tệp máy từ xa về máy mk<br>
- 'scp [tên ng dùng trên mt từ xa]@[IP của mt từ xa]:/home/[tên ng dùng trên mt từ xa]/[tên tệp trên mt từ xa] [tên tệp trên máy mk]'<br>

1. Now, use Python 3's "HTTPServer" module to start a web server in the home directory of the "tryhackme" user on the deployed instance.<br>
- chạy python3: python3 -m http.server<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/e09e2378-34f2-4ab6-b6c8-0bcccf94a16e)<br>

2. Download the file http://10.10.186.89:8000/.flag.txt onto the TryHackMe AttackBox<br>
- 'wget http://10.10.186.89:8000/.flag.txt':<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/acbcd300-daae-471e-a77b-78e163d9abdf)<br>

- cat file -> As: THM{WGET_WEBSERVER}<br>

*. task 5<br>
- process: là các tiến trình đnag chạy đc quản lí bs nhân, mỗi tiến trình có 1 PID (chỉ số này tăng dần theo tt q.trình start)
- ps -aux: show các process đc chạy bs other user và những quy trình ko chạy từ 1 phiên (system processes)
- top: cc só liệu thống kê theo time thực, đc lm ms 10s/lần và khi bn xài phím mũi tên để duyệt các hàng khác nhau
- quản lý process:<br>
1. sigterm: tắt tiến trình nma cho dọn dẹp trc
2. sigkill: hủy quy trình mà ko dọn dẹp
3. sigtop: dừng/tạm dừng 1 tiến trình<br>
- systemd: cung cấp cách quản lý các quy trình của ng dùng, nằm giữa hđh và ng dùng
- systemctl: cho phép tg tác vs process/daemon systemd
- cú pháp: systemctl [option] [service]
- option:<br>
1. start
2. stop
3. enable
4. disable<br>
- & = ctrl + z: tạo nền or tạm dừng việc thực thi lệnh (fg là đưa quay lại)<br>

1. If we were to launch a process where the previous ID was "300", what would the ID of this new process be?<br>
As: 301<br>

2. If we wanted to cleanly kill a process, what signal would we send it?<br>
As: sigterm<br>

3. Locate the process that is running on the deployed instance (10.10.186.89). What flag is given?<br>
- xài 'ps aux':<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/566252a3-faf5-4fdc-81bd-d14143e58ead)<br>

As: THM{PROCESSES}<br>

4. What command would we use to stop the service "myservice"?<br>
As: systemctl stop myservice<br>

5. What command would we use to start the same service on the boot-up of the system?<br>
As: systemctl enable myservice<br>

6. What command would we use to bring a previously backgrounded process back to the foreground?<br>
As: fg<br>

*. task 6<br>
- lên lịch cho hành động/tác vụ -> xài quy trình cron thông qua crontabs
- crontabs yêu cầu 6 giá trị:<br>
1. MIN: phút thực hiện
2. HOUR: giờ thực hiện
3. DOM: ngày trong tháng
4. MON: tháng trong năm
5. DOW: ngày trong tuần
6. CMD: lệnh sẽ đc thực thi<br>
- giá trị nào ko quan tâm thay bằng '*'
- crontabs -e: để xửa crontab<br>

1. When will the crontab on the deployed instance (10.10.186.89) run?<br>
- xài 'crontab -e':<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/b9d0ea55-18a7-4f51-9518-f45ef1ee8bac)<br>

As: @reboot<br>

*. task 8<br>
1. Look for the apache2 logs on the deployable Linux machine<br>
- 'cd /var/log/apache2'<br>

2. What is the IP address of the user who visited the site?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/3990c8a8-fea9-4206-95a2-b90cebf0444f)<br>

- 'cat access.log.1':<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/f6d0faa8-a291-40e3-94f3-e0d62d290a9f)<br>

As: 10.9.232.111<br>

3. What file did they access?<br>
As: catsanddogs.jpg<br>
