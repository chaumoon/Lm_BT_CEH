- link bt: https://tryhackme.com/room/redteamrecon<br>

*. task 3<br>
- nhập lệnh: whois thmredteam.com<br>
1. When was thmredteam.com created (registered)? (YYYY-MM-DD)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/bfb5f3f1-cf38-4f20-8d39-18c82b59a419)<br>

As: 2021-09-24<br>

2. To how many IPv4 addresses does clinic.thmredteam.com resolve?<br>
- nhập lệnh: nslookup -type=A clinic.thmredteam.com<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/294f14d9-92d4-411c-8537-0c3ed346ccc1)<br>

As: 2<br>

3. To how many IPv6 addresses does clinic.thmredteam.com resolve?<br>
- nhập lệnh: nslookup -type=AAAA clinic.thmredteam.com<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/e9ea4e29-d68f-4d28-aee7-efefa98e8a35)<br>

As: 2<br>

*. task 4<br>
. một số cách sửa đổi tìm kiếm phổ biến:<br>
- "search phrase": tìm kết quả vs cụm từ chính xác
- osint filetype:pdf: tìm các tệp loai pdf liên quan đến 1 thuật ngữ nhất định
- salary site:blog.tryhackme.com: lim kết quả tìm kiếm cho 1 trang web cụ thể
- pentest -site:example.com: loại trừ 1 trang web cụ thể khỏi kết quả
- walkthrough intitle:TryHackMe: tìm các trang web có thuật ngữ cụ thể trong tiêu đề trang
- challenge inurl:tryhackme: tìm các trang có cụm từ cụ thể trong URL trang<br>

. một số công cụ để tìm kiếm<br>
- https://www.google.com/advanced_search
- https://support.google.com/websearch/answer/2466433
- https://help.duckduckgo.com/duckduckgo-help-pages/results/syntax/
- https://help.bing.microsoft.com/apex/index/18/en-US/10002
- https://www.exploit-db.com/google-hacking-database
- https://tryhackme.com/room/googledorking<br>

. google hacking database (GHDB)<br>
- xem nhật kí: https://www.exploit-db.com/ghdb/6364
- khám phá tệp rò rỉ in4: https://www.exploit-db.com/ghdb/7047
- tìm khóa RSA riêng tư có bị lộ ko: https://www.exploit-db.com/ghdb/6768
- tìm in4 máy chủ: https://www.exploit-db.com/ghdb/6876
- định vị các tệp php: https://www.exploit-db.com/ghdb/7786
- k.phá bảng điều khiển web: https://www.exploit-db.com/ghdb/6728
- tìm tệp nhật kí liên quan đến lỗi: https://www.exploit-db.com/ghdb/5963<br>

1. How would you search using Google for xls indexed for http://clinic.thmredteam.com?<br>
As: filetype:xls site:clinic.thmredteam.com<br>

2. How would you search using Google for files with the word passwords for http://clinic.thmredteam.com?<br>
As: passwords site:clinic.thmredteam.com<br>

*. task 5<br>
. công cụ tìm kiếm đặc biệt:<br>
- truy cứu IP ngc (bắt đầu từ 1 tên miền or IP -> tên miền khác = địa chỉ IP cụ thể): https://viewdns.info/
- cung cấp tên miền or đại chỉ IP -> khởi chạy thử nghiệm từ check phần mềm độc hại đến truy vấn whois và DNS: https://threatintelligenceplatform.com/
- cung cấp in4 về địa chỉ IP và tên miền: https://search.censys.io/
- shodan đc xài từ dòng lệnh terminal: https://www.shodan.io/<br>

1. What is the shodan command to get your Internet-facing IP address?<br>
- nhập lệnh: shodan -h<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/c79a8b66-22f6-46bc-8615-ab692cb51d3a)<br>

As: shodan myip<br>

*. task 6<br>
- là 1 framework tự động hóa việc osint
- các bước: xem trong link bt tryhackme<br>

1. How do you start recon-ng with the workspace clinicredteam?<br>
As: recon-ng -w clinicredteam<br>

2. How many modules with the name virustotal exist?<br>
- nhập lệnh: marketplace search virustotal<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/2de65bb1-75ad-4354-8c2c-66f10af0bb50)<br>

As: 2<br>

3. There is a single module under hosts-domains. What is its name?<br>
- nhập lệnh: marketplace search hosts-domains<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/6f893d9e-edb3-4c4d-b5c7-db65e259e19f)<br>

As: migrate_hosts<br>

4. censys_email_address is a module that “retrieves email addresses from the TLS certificates for a company.” Who is the author?<br>
- nhập lệnh: marketplace info censys_email_address<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/32e9d592-bde8-4604-a09a-c589503ff8bb)<br>

As: Censys Team<br>

*. task 7<br>
- công cụ: https://www.maltego.com/transform-hub/<br>
1. What is the name of the transform that queries NIST’s National Vulnerability Database?<br>
As: nist nvd<br>

2. What is the name of the project that offers a transform based on ATT&CK?<br>
As: misp project
