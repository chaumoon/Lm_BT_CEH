- link bt: https://tryhackme.com/room/nmap01
- còn nh phòng nx có time sẽ hoàn thiện<br>

*. task 1<br>
- các cách tiếp cận nmap xài để khám phá máy chủ trực tiếp:<br>
. ARP scan<br>
. ICMP scan<br>
. TCP/UDP ping scan<br>

*. task 2<br>
- phân đoạn mạng đề cập đến kết nối vật lý
- mạng con đề cập đến kết nối logic
- mạng con có /16: subnet mask đc viết là 255.255.0.0 (khoảng 65k máy chủ)
- mạng con có /24: subnet mask ddc viết là 255.255.255.0 (khoảng 250 máy chủ)<br>

1. How many devices can see the ARP Request?<br>
As: 4<br>

2. Did computer6 receive the ARP Request? (Y/N)<br>
As: N<br>

3. How many devices can see the ARP Request?<br>
As: 4<br>

4. Did computer6 reply to the ARP Request? (Y/N)<br>
As: Y<br>

*. task 3<br>
- vd về đặc tả mục tiêu:<br>
. list: MACHINE_IP scanme.nmap.org example.com -> quét 3 địa chỉ IP<br>
. range: 10.11.12.15-20 -> quét 6 địa chỉ IP là 10.11.12.15, 10.11.12.16,… và 10.11.12.20<br>
. subnet: MACHINE_IP/30 -> quét 4 địa chỉ IP (1 địa chỉ 32 bits /30 bits -> còn 2 bits -> 2^2)<br>
- can cung cấp tệp lm đầu vào cho list mục tiêu: nmap -iL list_of_hosts.txt
- check list máy chủ nmap sẽ quét: nmap -sL TARGETS
- nmap thử phân giải DNS ngc -> tên can lộ nhiều in4 (ko muốn nmap đến máy chủ DNS ta thêm -n)<br>

1. What is the first IP address Nmap would scan if you provided 10.10.12.13/29 as your target?<br>
As: 10.10.12.8<br>

2. How many IP addresses will Nmap scan if you provide the following range 10.10.0-255.101-125? <br>
As: 256*25=6400<br>

*. task 4<br>
- trong TCP/IP:<br>
. ARP from link layer<br>
. ICMP from network layer<br>
. TCP from transport layer<br>
. UDP from transport layer<br>
- tác dụng:<br>
. ARP: gửi 1 frame đến địa chỉ quảng bá trên phân đoạn mạng và yêu cầu mt có địa chỉ IP cụ thể phản hồi bằng cách cung cấp địa chỉ MAC của nó<br>
. ICMP ping xài type 8 (echo) và type 0 (echo reply)<br>
. muốn ping 1 hệ thống trên cùng 1 mạng con, 1 truy vấn ARP nên đặt trước ICMP echo<br>
. máy quét can gửi 1 gói đặc biệt đến các cổng TCp và UDP chung để chekc mục tiêu phản hồi hay ko (hiệu quả, đặc biệt khi ICMP echo bị chặn)<br>

1. What is the type of packet that computer1 sent before the ping?<br>
As: arp request<br>

2. What is the type of packet that computer1 received before being able to send the ping?<br>
As: arp response<br>

3. How many computers responded to the ping request?<br>
As: 1<br>

4. What is the name of the first device that responded to the first ARP Request?<br>
As: router<br>

5. What is the name of the first device that responded to the second ARP Request?<br>
As: computer5<br>

6. Send another Ping Request. Did it require new ARP Requests? (Y/N)<br>
As: N<br>

*. task 5<br>
- phg pháp để khám phá máy chủ trực tiếp:<br>
. ng dùng đặc quyền -> xài ARP requests<br>
. ng dùng đặc quyền quét mục tiêu bên ngoài mạng cục bộ -> xài yêu cầu ICMP echo, TCP ACk (80), TCP SYN (443) và yêu cầu dấu time ICMP<br>
. ng dùng ko đặc quyền quét mục tiên bên ngoài mạng cục bộ -> xài bắt tay 3 bc <br>
- theo mặc định nmap dùng ping scan để quét máy chủ trực tiếp
- muốn quét máy chủ trực tuyến mà ko quét cổng của các hệ thống trực tiếp -> xài nmap -sn targets
- chỉ can quét ARP nếu ở trong cùng mạng con vs hệ thống đích
- trên ethernet (802.3), wifi (802.11) cần bt địa chỉ MAC
- chỉ quét ARP mà ko quét cổng: nmap -PR -sn targets
- quét ARP can xài: arp -scan<br>

1. How many devices are you able to discover using ARP requests?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/9fe5c685-50fa-4ba0-9672-3c92b30e1a6f)<br>

As: 3<br>

*. task 6<br>
- để xài ICMP echo request ta thêm: -PE
- ICMP echo thg bị chặ -> thêm ICMP timestamp hoặc ICMP address mask requests để xem hệ thống có trực tuyến hay ko<br>

1. What is the option required to tell Nmap to use ICMP Timestamp to discover live hosts?<br>
As: -PP<br>

2. What is the option required to tell Nmap to use ICMP Address Mask to discover live hosts?<br>
As: -PM<br>

3. What is the option required to tell Nmap to use ICMP Echo to discover life hosts?<br>
As: -PE<br>

*. task 7<br>
. TCP SYN ping:<br>
- hình thức hoạt động: bắt tay 3 bc
- ng dùng đặc quyền can gửi các gói TCP SYN và ko cần hoàn thành quá trình bắt tay 3 bc ngay cả khi cổng mở, còn ng dùng ko đặc quyền phải hoàn thành<br>
. TCP ACK ping<br>
- hệ thống mở -> phản hồi cờ RST
- đang ngoại tuyến or ko thể truy cập -> ko phản hồi<br>
. UDP ping<br>
. masscan<br>
- tốc độ, can kết thúc quá trình quét mạng 1 cách nhanh chóng<br>

1. Which TCP ping scan does not require a privileged account?<br>
As: TCP SYN ping<br>

2. Which TCP ping scan requires a privileged account?<br>
As: TCP ACK ping<br>

3. What option do you need to add to Nmap to run a TCP SYN ping scan on the telnet port?<br>
As: -PS23<br>

*. task 8<br>
1. We want Nmap to issue a reverse DNS lookup for all the possibles hosts on a subnet, hoping to get some insights from the names. What option should we add?<br>
As: -R
