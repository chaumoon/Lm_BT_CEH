- link bt: https://tryhackme.com/room/rustscan<br>

*. task 1<br>
- công cụ quét cổng<br>

*. task 4<br>
- rustscan nhanh vì: <br>
. mạng hạt nhân cấp thấp<br>
. viết bằng ngôn ngữ nhanh (rust)<br>
. quét ko đồng bộ, đa luồng bị chậm do chi phí chuyển đổi ngữ cảnh. Async rất nhanh<br>

*. task 5<br>
- rustscan can mở rộng bằng RustScan Scripting Engine (RSE) -> cho phép viết 1 tập lệnh chạy sau khi quá trình quét hoàn tất, lấy đầu vào của các cổng mở và IP tương ứng của chúng
- RSE hỗ trợ các ngôn ngữ sau: <br>
. python<br>
. Shell<br>
. Perl<br>
. bất kỳ chg trình nào là nhị phân và ở dạng $PATH<br>
- công cụ tạo tập lệnh của rustscan can đc thay đổi = cách xài đối số "--script"
- có 3 lý lẽ can xảy ra:<br>
. none: ko chạy bất kỳ tập lệnh nào<br>
. custom: chạy all các tập lệnh trong thư mục tập lệnh<br>
. default: chạy bất kỳ tập lệnh nào có trong tệp cấu hình, ko cần bật mặc định vì nó đc bật theo mặc định<br>
1. tập lệnh tùy chỉnh python:<br>
- để thực thi -> cần tệp Rustscan_scripts.toml có tại $HOME/.rustscan_scripts.toml
- vd:<br>
```
# Test/Example ScriptConfig file

# Tags to filter on scripts. Only scripts containing all these tags will run.
tags = ["core_approved", "example"]

# If it's present then only those scripts will run which has a tag ports = "80". Not yet implemented.
#
# ex.:
# ports = ["80"]
# ports = ["80","81","8080"]
ports = ["80"]

# Only this developer(s) scripts to run. Not yet implemented.
developer = ["example"]
```

- tập lệnh python cơ bản để tham khảo:<br>

```
#!/usr/bin/python3
#tags = ["core_approved", "example",]
#developer = [ "example", "https://example.org" ]
#trigger_port = "80"
#call_format = "python3 {{script}} {{ip}} {{port}}"

# Scriptfile parser stops at the first blank line with parsing.
# This script will run itself as an argument with the system installed python interpreter, only scanning port 80.
# Unused filed: ports_separator = ","

import sys

print('Python script ran with arguments', str(sys.argv))
```
2. tags<br>
- tag là các loại tập lệnh, có các loại:<br>
. HTTP<br>
. SSH<br>
. tomcat<br>
- để chạy tập lệnh -> tệp cấu hình sẽ chỉ thực thi các tập lệnh có danh mục phù hợp<br>
3. Developer<br>
- thẻ này để chỉ ra ai là ng phát triển tập lệnh<br>
4. Trigger Point<br>
- thẻ này nêu rõ tập lệnh sẽ kích hoạt cổng nào<br>
5. Call Format<br>
- rustscan xài thư viện tạo khuôn mẫu: text_placeholder (https://crates.io/crates/text_placeholder)
- cho phép c.ta dặt các biến trong dấu {{}} ({{variable}})
- rustscan hỗ trợ 3 biến:<br>
. The script name<br>
. The IP address<br>
. The port(s)<br>
```
#call_format = "python3 {{script}} {{ip}} {{port}}"
```
6. The Code itself<br>
- baayh all thứ sau siêu dữ liệu này là mã
- tập lệnh sẽ nhận các đối số qua sys.argv ở định dạng đc chỉ định trong biến call_format<br>
*. Contributing / Making Scripts<br>
- thư mục chứa các tập lệnh mẫu: https://github.com/RustScan/RustScan/tree/master/fixtures/.rustscan_scripts<br>
7. Running Other Tools with RustScan<br>
- đa số đều can chạy vs rustscan
- để thực thi 1 chg trình khác -> tạo tập lệnh shell gọi chg trình đó
- vd:<br>
```
nmap -vvv -p {{port}} {{ip}}
```
1. What is the scripting file config called?<br>
As: rustscan_scripts.toml<br>

2. Can you run other binaries with RustScan? (T)rue / (F)alse.<br>
As: T<br>

3. Does RutScan support scripts in Javascript? (T)rue / (F)alse.<br>
As: F<br>

*. task 6<br>
- rustscan ko quét 1000 cổng đầu tiên mà nó tùy chỉnh để quét các cổng phù hợp<br>

*. task 7<br>
- quét và chuyển đầu ra sang nmap: rustscan -r ports -a  <Target-ip> -- <nmap cmds><br>
- những việc can làm:<br>
. quét nh IP: rustscan -a 127.0.0.1,0.0.0.0 (phân tách băng dấu ',')<br>
. quét máy chủ: <br>
```
➜ rustscan -a www.google.com, 127.0.0.1
Open 216.58.210.36:1
Open 216.58.210.36:80
Open 216.58.210.36:443
Open 127.0.0.1:53
Open 127.0.0.1:631
```
. rustscan hỗ trợ CIDR: ➜ rustscan -a 192.168.0.0/30<br>
. tập tin máy chủ lm đầu vào: (list IP/máy chủ đc phân tách bằng dòng ms để quét) <br>
host.txt<br>
```
192.168.0.1
192.168.0.2
google.com
192.168.0.0/30
127.0.0.1
```
đối số là: rustscan -a 'hosts.txt'<br>
. quét cổng riêng lẻ: ➜ rustscan -a 127.0.0.1 -p 53
53<br>
. quét nh cổng đã chọn: ➜ rustscan -a 127.0.0.1 -p 53,80,121,65535
53<br>
. phạm vi cổng: (để quét 1 loạt các cổng) ➜ rustscan -a 127.0.0.1 --range 1-1000    
53,631<br>
. điều chỉnh các đối số nmap:<br>
điều chỉnh: rustscan -a 127.0.0.1 -- -A -sC<br>
chạy: nmap -Pn -vvv -p $PORTS -A -sC 127.0.0.1<br>
. thứ tự cổng ngẫu nhiên: (giúp ko tắt tg lửa) ➜ rustscan -a 127.0.0.1 --range 1-1000 --scan-order "Random"
53,631<br>

1. After scanning this, how many ports do we find open under 1000?
- chạy: rustscan -a 10.10.221.112<br>
```
┌──(root㉿kali)-[/home/kali/Downloads]
└─# rustscan -a 10.10.221.112                                        
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.221.112:22
Open 10.10.221.112:80
[~] Starting Nmap
[>] The Nmap command to be run is nmap -vvv -p 22,80 10.10.221.112

Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 11:21 EDT
Initiating Ping Scan at 11:21
Scanning 10.10.221.112 [4 ports]
Completed Ping Scan at 11:21, 0.28s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:21
Completed Parallel DNS resolution of 1 host. at 11:21, 0.01s elapsed
DNS resolution of 1 IPs took 0.02s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 11:21
Scanning 10.10.221.112 [2 ports]
Discovered open port 22/tcp on 10.10.221.112
Discovered open port 80/tcp on 10.10.221.112
Completed SYN Stealth Scan at 11:21, 0.27s elapsed (2 total ports)
Nmap scan report for 10.10.221.112
Host is up, received reset ttl 63 (0.25s latency).
Scanned at 2023-09-29 11:21:36 EDT for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.77 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (128B)
```
As: 2<br>

2. Perform a service version detection scan, what is the version of the software running on port 22?<br>
```
┌──(root㉿kali)-[/home/kali/Downloads]
└─# nmap -v -sC -sV 10.10.221.112 -p 22
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 11:26 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 11:26
Completed NSE at 11:26, 0.00s elapsed
Initiating NSE at 11:26
Completed NSE at 11:26, 0.00s elapsed
Initiating NSE at 11:26
Completed NSE at 11:26, 0.00s elapsed
Initiating Ping Scan at 11:26
Scanning 10.10.221.112 [4 ports]
Completed Ping Scan at 11:26, 0.27s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:26
Completed Parallel DNS resolution of 1 host. at 11:26, 0.01s elapsed
Initiating SYN Stealth Scan at 11:26
Scanning 10.10.221.112 [1 port]
Discovered open port 22/tcp on 10.10.221.112
Completed SYN Stealth Scan at 11:26, 0.27s elapsed (1 total ports)
Initiating Service scan at 11:26
Scanning 1 service on 10.10.221.112
Completed Service scan at 11:26, 0.52s elapsed (1 service on 1 host)
NSE: Script scanning 10.10.221.112.
Initiating NSE at 11:26
Completed NSE at 11:27, 7.60s elapsed
Initiating NSE at 11:27
Completed NSE at 11:27, 0.01s elapsed
Initiating NSE at 11:27
Completed NSE at 11:27, 0.00s elapsed
Nmap scan report for 10.10.221.112
Host is up (0.25s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 c1:c5:15:c8:74:67:b3:3a:52:0a:0b:1c:95:ca:9b:ec (DSA)
|   2048 14:1c:09:29:a7:32:d6:0b:99:0f:a6:e9:4b:4c:c6:93 (RSA)
|   256 75:86:5e:88:e8:20:59:a7:26:e0:bf:64:d1:74:86:c0 (ECDSA)
|_  256 6b:9c:91:74:5d:27:d3:a5:64:b6:cc:8f:cf:12:41:93 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 11:27
Completed NSE at 11:27, 0.00s elapsed
Initiating NSE at 11:27
Completed NSE at 11:27, 0.00s elapsed
Initiating NSE at 11:27
Completed NSE at 11:27, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.28 seconds
           Raw packets sent: 5 (196B) | Rcvd: 2 (84B)
```
As: 6.6.1p1<br>

3. Perform an aggressive scan, what flag isn't set under the results for port 80?<br>
```
┌──(root㉿kali)-[/home/kali/Downloads]
└─# nmap -v -sC -sV 10.10.221.112 -p 80
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 11:31 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Initiating Ping Scan at 11:31
Scanning 10.10.221.112 [4 ports]
Completed Ping Scan at 11:31, 0.44s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:31
Completed Parallel DNS resolution of 1 host. at 11:31, 0.01s elapsed
Initiating SYN Stealth Scan at 11:31
Scanning 10.10.221.112 [1 port]
Discovered open port 80/tcp on 10.10.221.112
Completed SYN Stealth Scan at 11:31, 0.28s elapsed (1 total ports)
Initiating Service scan at 11:31
Scanning 1 service on 10.10.221.112
Completed Service scan at 11:31, 6.57s elapsed (1 service on 1 host)
NSE: Script scanning 10.10.221.112.
Initiating NSE at 11:31
Completed NSE at 11:31, 4.89s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 1.04s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Nmap scan report for 10.10.221.112
Host is up (0.26s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.7 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/
|_http-favicon: Unknown favicon MD5: 69C728902A3F1DF75CF9EAC73BD55556
| http-title: Login :: Damn Vulnerable Web Application (DVWA) v1.10 *Develop...
|_Requested resource was login.php

NSE: Script Post-scanning.
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Initiating NSE at 11:31
Completed NSE at 11:31, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.94 seconds
           Raw packets sent: 5 (196B) | Rcvd: 2 (72B)
```
As: httponly<br>

*. task 8<br>
1. First, how do you access the help menu?<br>
As: -h<br>

2. Often referred to as "quiet" mode, What switch can do this?<br>
As: -q<br>

3. Which switch can help us to scan for a particular Range?<br>
As: -r<br>

4. What switch would you use to find out RustScan's version?<br>
As: -v<br>

5. Which switch will help us to select batch size?<br>
As: -b<br>

6. Which switch can set timeout?<br>
As: -t
