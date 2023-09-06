- link bt: https://tryhackme.com/room/metasploitintro<br>

*. task 1<br>
- can hõ trợ từ quá trình tham gia thử nghiệm thâm nhập, thu thập in4 đến hậu khai thác
- bản dùng để học tập: tập trung vào miền thử nghiệm thâm nhập, hữu ích cho việc nghiêm cứu lỗ hổng và phát triển khai thác
- các thành phần chính của metasploit framework: modeles, tools, msfconsole<br>

*. task 2<br>
- modele đc xây dựng để thực hiện 1 nhiệm vụ cụ thể: khai thác lỗ hổng, quét mục tiêu, thực hiện 1 cuộc tấn công<br>

1. What is the name of the code taking advantage of a flaw on the target system?<br>
As: Exploit<br>

2. What is the name of the code that runs on the target system to achieve the attacker's goal?<br>
As: payload<br>

3. What are self-contained payloads called?<br>
As: Singles<br>

4. Is "windows/x64/pingback_reverse_tcp" among singles or staged payload?<br>
As: singles<br>

*. task 3<br>
- xài -> dòng lệnh thành msf6 or msf5 tùy phiên bản<br>

1. How would you search for a module related to Apache?<br>
As: search apache<br>

2. Who provided the auxiliary/scanner/ssh/ssh_login module?<br>
- nhập lệnh: use auxiliary/scanner/ssh/ssh_login<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/5e21e7cd-41c4-451d-8d2c-ce62196ca813)<br>

- info:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/e1583e0c-c467-477a-a1f4-a2fe1d2bd3b2)<br>

As: todb<br>

*. task 4<br>
- đặt tham số bằng cú pháp: set parameter_name value
- xài set (chuyển module sẽ mất giá trị), xài setg (chuyển module vẫn ok)<br>

1. How would you set the LPORT value to 6666?<br>
As: set lport 6666<br>

2. How would you set the global value for RHOSTS  to 10.10.19.23 ?<br>
As: setg rhosts 10.10.19.23<br>

3. What command would you use to clear a set payload?<br>
As: unset payload<br>

4. What command do you use to proceed with the exploitation phase?<br>
As: exploit
