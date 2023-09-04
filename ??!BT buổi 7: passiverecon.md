- link bt: https://tryhackme.com/room/passiverecon
- ở đây có một chuỗi phòng chưa hoàn thành<br>

*. task 2<br>
1. You visit the Facebook page of the target company, hoping to get some of their employee names. What kind of reconnaissance activity is this? (A for active, P for passive)<br>
As: P<br>

2. You ping the IP address of the company webserver to check if ICMP traffic is blocked. What kind of reconnaissance activity is this? (A for active, P for passive)<br>
As: A<br>

3. You happen to meet the IT administrator of the target company at a party. You try to use social engineering to get more information about their systems and network infrastructure. What kind of reconnaissance activity is this? (A for active, P for passive)<br>
As: A<br>

*. task 3<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/d30868b9-4daa-4e79-a333-c2468fab321d)<br>

1. When was TryHackMe.com registered?<br>
As: 20180705<br>

2. What is the registrar of TryHackMe.com?<br>
As: namecheap.com<br>

3. Which company is TryHackMe.com using for name servers?<br>
As: CLOUDFLARE.COM<br>

*. task 4<br>
- nslookup and dig:<br>
. A: địa chỉ IPv4<br>
. AAAA: địa chỉ IPv6<br>
. CNAME: tên chuẩn<br>
. MX: máy chủ mail<br>
. SOA: bắt đầu ủy quyền<br>
. TXT: bản ghi TXT<br>

1. Check the TXT records of thmlabs.com. What is the flag there?<br>
- chạy lệnh: nslookup -type=TXT thmlabs.com<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/bbc17413-a45f-45a6-8f29-57a4318ef7c8)<br>

As: THM{a5b83929888ed36acb0272971e438d78}<br>

*. task 5<br>
- công cụ: https://dnsdumpster.com/<br>

1. Lookup tryhackme.com on DNSDumpster. What is one interesting subdomain that you would discover in addition to www and blog?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/dd3f81c7-5559-4bd8-a624-4d6d716a0f2b)<br>

As: remote<br>

*. task 6<br>
- công cụ: https://www.shodan.io/<br>

1. According to Shodan.io, what is the 2nd country in the world in terms of the number of publicly accessible Apache servers?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/19455656-d827-4d5e-bb33-e2145a61c2c9)<br>

As: Germany<br>

2. Based on Shodan.io, what is the 3rd most common port used for Apache?<br>
As: 8080<br>

3. Based on Shodan.io, what is the 3rd most common port used for nginx?<br>
As: 888<br>
