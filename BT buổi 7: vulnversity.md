- link bài tập: https://tryhackme.com/room/vulnversity<br>

*. task 2<br>
- nmap:<br>
. -sV: xác định phiên bản của dịch vụ đang chạy<br>
. -p (x) or -p-: quét cổng để tìm cổng x or all cổng<br>
. -Pn: tắt tính năng phát hiện máy chủ và quét các cổng đang mở<br>
. -A: xác định hđh và phiên bản, thực thi các tập lệnh trong bản dựng để liệt kê thêm<br>
. -sC : quét bằng tập lệnh nmap mặc định<br>
. -v: chế độ verbose<br>
. -sU: quét cổng UDP<br>
. -sS: quét cổng TCP SYN<br>

1. Scan the box; how many ports are open?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/9132e5d0-0ccb-4721-b88a-6fc512055488)<br>

As: 6<br>

2. What version of the squid proxy is running on the machine?<br>
As: 3.5.12<br>

3. How many ports will Nmap scan if the flag -p-400 was used?<br>
As: 400<br>

4. What is the most likely operating system this machine is running?<br>
As: Ubuntu<br>

5. What port is the web server running on?<br>
As: 3333<br>

6. What is the flag for enabling verbose mode using Nmap?<br>
As: -v<br>

*. task 3<br>
- gobuster<br>
. -e: in URL đầy đủ trong bảng điều khiển của bạn<br>
. -u: URL mục tiêu<br>
. -w: đg dẫn đến danh sách từ của bạn<br>
. -U và -P: tên ng dùng và mật khẩu cho xác thực cơ bản<br>
. -p (x): proxy để xài cho các yêu cầu<br>
. -c (http cookies): chỉ định cookies để mô phỏng xác thực của bạn<br>

1. What is the directory that has an upload form page?<br>
- xài lệnh: dirsearch -u http://10.10.21.83:3333<br>
As: /internal/<br>
- page này kp trang nào cx có, mấy cái khác là trang nào cx có<br>

*. task 4<br>
1. What common file type you'd want to upload to exploit the server is blocked? Try a couple to find out.<br>
As: .php<br>

- xài burpsuite<br>
1. tạo file reverse<br>
- dùng tool rev (php pentestmonkey) + IP máy tryhackme và cổng tùy ý
- copy nội dung file rev tạo 1 file .php trong kali<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/73c6a6da-2480-4df8-9d7c-292a682ff105)<br>

2. chặn request<br>
- chạy burpsuite trong kali
- upload file vừa tạo lên để chặn request<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/8ec1ca80-8693-4c09-874e-2871dd92104c)<br>

3. lm theo các bc như trong tryhackme để thu đc kết quả<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/7c9f8923-529b-419d-a76d-8fb30b5a761d)<br>

2. Run this attack, what extension is allowed?<br>
As: .phtml<br>

3. What is the name of the user who manages the webserver?<br>
- tải file php-reverse-shell.php về
- đổi ip thành ip tun0 của mk (ip a s đê xem ip tun0) và .php thành phtml
- upload file lên và chờ lệnh nghe nc -lnvp 1234:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/1bf11d4e-455f-4a9c-b690-3755bdb091b2)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/43d181c8-700e-4021-a9c5-374ca67724b6)<br>

As: bill<br>

4. What is the user flag?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/32b4047e-0df5-4fe8-9301-c2215e7108e2)<br>

As: 8bd7992fbe8a6ad22a63361004cfcedb<br>

*. task 5<br>
1. On the system, search for all SUID files. Which file stands out?<br>
- chạy lệnh: find / -perm /4000 2>/dev/null<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/a10d4faa-8142-451d-9e07-400e05c4d9ca)<br>

As: /bin/systemctl<br>

2. Become root and get the last flag (/root/root.txt)<br>
- chữa sau


