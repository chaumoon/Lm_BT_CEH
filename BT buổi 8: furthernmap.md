- link bt: https://tryhackme.com/room/furthernmap<br>

*. task 2<br>
- việc đầu tiên cần lm là quét cổng
- mỗi mt có tổng cộng 65535 cổng khả dụng<br>

. một số cổng tiru chuẩn:<br>
- http: 80
- https: 443
- windows NETBIOS: 139
- SMB: 445<br>

1. What networking constructs are used to direct traffic to the right application on a server?<br>
As: ports<br>

2. How many of these are available on any network-enabled computer?<br>
As: 65535<br>

3. [Research] How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task)<br>
As: 1024<br>

*. task 3<br>
- xài lệnh: nmap -h<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/d7a82f5a-4fc6-4117-895e-2bde30e6be2b)<br>

1. What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?<br>
As: -sS<br>

2. Which switch would you use for a "UDP scan"?<br>
As: -sU<br>

3. If you wanted to detect which operating system the target is running on, which switch would you use?<br>
As: -O<br>

4. Nmap provides a switch to detect the version of the services running on the target. What is this switch?<br>
As: -sV<br>

5. The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?<br>
As: -v<br>

6. Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?
(Note: it's highly advisable to always use at least this option)<br>
As: -vv<br>

7. What switch would you use to save the nmap results in three major formats?<br>
As: -oA<br>

8. What switch would you use to save the nmap results in a "normal" format?<br>
As: -oN<br>

9. A very useful output format: how would you save results in a "grepable" format?<br>
As: -oG<br>

10. Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning. How would you activate this setting?<br>
As: -A<br>

11. Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!
How would you set the timing template to level 5?<br>
As: -T5<br>

12. How would you tell nmap to only scan port 80?<br>
As: -p 80<br>

13. How would you tell nmap to scan ports 1000-1500?<br>
As: -p 1000-1500<br>

14. How would you tell nmap to scan all ports?<br>
As: -p-<br>

15. How would you activate a script from the nmap scripting library (lots more on this later!)?<br>
As: --script<br>

16. How would you activate all of the scripts in the "vuln" category?<br>
As: --script=vuln<br>

*. task 5<br>
- nmap kết nối vs từng cổng TCp và xác định xem d.vụ mở or đóng bằng phản hồi mà nó nhận đc
- gửi tới TCP vs gói SYN: cổng đóng (phản hồi cờ RST), cổng mở (phản hồi cờ SYN/ACK)
- nếu ko nhận đc phản hồi -> cổng đang đc bảo vệ bởi tường lửa (cổng đã đc lọc)
- chuyển tg lửa phản hồi vs gói RST TCP: iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset<br>

1. Which RFC defines the appropriate behaviour for the TCP protocol?<br>
As: RFC 9293<br>

2. If a port is closed, which flag should the server send back to indicate this?<br>
As: RST<br>

*. task 6<br>
- dùng để quét p.vi cổng TCp của 1 or nh mục tiêu<br>
. ưu điểm:<br>
- bỏ qua các hệ thống phát hiện xâm nhập cũ khi tìm kiếm 1 cái bắt tay 3 bc đầy đủ
- ps: ko xảy ra vs các giải pháp IDS hiện đại
- quét lén lút, ko đc ghi lại bởi các ứng dụng đang nghe trên các cổng mở (vì thg chỉ ghi lại kết nối khi nó đc thiết lập đầy đủ
- SYN nhanh hơn scan TCP<br>
. nhược điểm:<br>
- cần quyền sudo
- ko ổn dịnh
- nmap: có sudo (mặc định -sS), ko có sudo (mặc định -sT)<br>

1. There are two other names for a SYN scan, what are they?<br>
As: Half-open, Stealth<br>

2. Can Nmap use a SYN scan without Sudo permissions (Y/N)?<br>
As: N<br>

*. task 7<br>
- kết nối UDP là kết nối ko trạng thái
- UDP gửi các gói ts cổng mục tiêu và hi vọng rằng chúng thực hiện đc
- UDP: tốc độ > chất lg
- thiếu xác thực -> khó quét
- cổng mở (UDP ko phản hồi), cổng đóng (phản hồi bằng gói ICMP)
- UDP: chậm<r>

1. If a UDP port doesn't respond to an Nmap scan, what will it be marked as?<br>
As: open|filtered<br>

2. When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?<br>
As: ICMP<br>

*. task 8<br>
- quét lén lút hơn -sS
- (-sN); khi yêu cầu TCP đc gửi mà ko có cờ nào đc đặt
- theo RSC: cổng đóng -> phản hồi RST
- (-sF): yêu cầu gửi vs cờ FIN: xài để đóng 1 kết nối đang hoạt động, cổng đóng -> phản hồi RST
- (-sX): gửi gói TCP sai định dạng, cổng đóng -> RST
- cổng mở -> ko phản hồi d.vs gói sai định dạng, cổng đc bảo vệ bởi tg lửa nó cx ko phản hồi<br>

1. Which of the three shown scan types uses the URG flag?<br>
As: xmas<br>

2. Why are NULL, FIN and Xmas scans generally used?<br>
As: firewall evasion<br>

3. Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?<br>
As: Microsoft Windows<br>

*. task 9<br>
- check xem địa chỉ IP nào chứa máy chủ đang hoạt động và cái nào ko<br>

1. How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation)<br>
As: nmap -sn 172.16.0.0/16<br>

*. task 10<br>
- aim: do thám<br>

1. What language are NSE scripts written in?<br>
As: lua<br>

2. Which category of scripts would be a very bad idea to run in a production environment?<br>
As: intrusive<br>

*. task 11<br>
1. What optional argument can the ftp-anon.nse script take?<br>
- chạy lệnh: nmap --script-help ftp-anon.nse:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/30e8b6c5-7e14-42ee-8010-7aa860a5992e)<br>

- truy cập vào đường link https hiện ra:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/76dcac45-7e94-40cd-a2c1-1ef8ea80b344)<br>

As: maxlist<br>

*. task 12<br>
- chạy lệnh: grep "smb" /usr/share/nmap/scripts/script.db<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/822c875e-553e-4137-8055-625483013f08)<br>

1. What is the filename of the script which determines the underlying OS of the SMB server?<br>
As: smb-os-discovery.nse<br>

2. Read through this script. What does it depend on?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/efad5ac4-8f44-4494-b823-9484a66f8c62)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/35188d43-80e5-4c3d-bfde-a223cafcc1f4)<br>

As: smb-brute<br>

*. task 13<br>
- nmap có tùy chọn -Pn: yêu cầu nmap ko bận tâm ping máy chủ trc khi quét nó
- -> coi máy chủ la còn sống và bỏ qua khối ICMP (mất nh time)
- nếu đang trực tiếp trên mạng cục bộ -> nmap can xài yêu cầu ARP để xác định hoạt động của máy chủ<br>
. một số switches cần lưu ý:<br>
- (-f): chia nhỏ các gói -> chúng ít bị tg lửa or IDS phát hiện
- (--mtu <number>): như -f nhưng kích thc đơn vị truyền tối đa để xài cho gói đc gửi chia hết cho 8
- (--scan-delay <time>ms): thêm độ trễ giữa các gói đc gửi, hữu ích khi mạng ko ổn định, can tránh bất kì trình kích hoạt tg lửa IDS dựa trên time nào can có
- (--badsum): tạo cổng check ko hợp lệ cho các gói, ngăn xếp TCP/IP thực loại bỏ gói này nhưng tg lửa có k.năng phản hồi tự động mà ko cần bận tâm đến việc tổng check của gói
- -> xài để xác định sự hiện diện của tg lửa IDS<br>

1. Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the -Pn switch?<br>
As: ICMP<br>

2. [Research] Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?<br>
As: --data-length<br>

*. task 14<br>
1. Does the target (10.10.66.242)respond to ICMP (ping) requests (Y/N)?<br>
- chạy lệnh: ping 10.10.66.242<br>

As: N<br>

2. Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?<br>
- chạy lệnh: nmap -sX -p 1-999 10.10.66.242<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/f1a9b28f-2e35-4107-bf5b-df9589684215)<br>

As: 999<br>

3. There is a reason given for this -- what is it?<br>
As: no response<br>

4. Perform a TCP SYN scan on the first 5000 ports of the target -- how many ports are shown to be open?<br>
- nhập lệnh: nmap -sS -Pn -p 1-5000 10.10.66.242<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/c6c7950b-735f-481e-9ab2-513876582b7a)<br>

As: 5<br>

5. Deploy the ftp-anon script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N)<br>
As: Y


