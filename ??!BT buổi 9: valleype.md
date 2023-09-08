- link bt: https://tryhackme.com/room/valleype<br>

*. quét và thu thập thông tin<br>
- quét cổng mở: rustscan -a 10.10.100.181 -- -sV -sC<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/3ac35afb-44e5-4938-be0d-851427920dc1)<br>

- truy cập và trang web server: 10.10.100.181<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/9c04b0bc-5885-42df-a8ce-5693cc1ad238)<br>
-> mò mẫn hồi cx chả ra gì :)))

- tìm các directory bằng dirsearch:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/4ce7870e-f660-48a8-a4d1-3e1c9fca58cb)<br>

- đi xem in4 và source của từng trang tìm ra:<br>

. http://10.10.100.181/gallery/ -> show các ảnh:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/77849631-0add-43a6-95af-1756c633c579)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/a072cbbe-e51a-43f0-aa82-0f783618eca0)<br>

-> dựa vào source -> static có ảnh, ...<br>

. http://10.10.100.181/static/<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/73d905cf-f977-4863-8731-dffbd0ffcbb0)<br>

-> chả có gì -> nó đã bị ẩn đi -> có điều bất thg<br>

- dùng lênh: dirsearch -u http://10.10.100.181/static/ để tìm thêm thông tin về URL này:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/6a2370df-ccc7-4dcf-95dd-7cc884d12155)<br>

- giờ check hêt mấy cái thu được nhé:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/0dd437c8-8c1c-49e8-a9e2-0c904c18d13f)<br>

- truy cập vào: http://10.10.88.11/dev1243224123123/<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/7a3b992b-cd28-4d9b-b046-ea0f7eed1ecd)<br>

- xem xét source của trang ta thu được:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/30a8ebd4-15cd-4232-864d-27a6f63996c2)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/c830ceed-2af3-4b9e-922f-cee15e0c9ea8)<br>

- thu thập tài khoản và truy cập vào URL vừa thu thập đc:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/2dd0c0c4-b065-46c6-9427-1d601f73e5aa)<br>

- bây giờ thử đăng nhập vào ftp bằng tài khoản vừa lấy về: ftp 10.10.88.11 37370<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/2d5e01cb-49b5-47b6-b90b-4a4bdbcb41f3)<br>

- xài ls -la thu được 3 file:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/cd3059fd-db41-4fdc-9120-fc1ad5ca6d9e)<br>

- lấy 3 file về máy: python3 -m http.server + wget http://10.10.88.11:37370/tên_file<br>

- xài wireshark lục tìm thông tin trong 3 file ta thu được:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/2291ba5f-df28-4b70-bce9-0f3f7a56c54a)<br>

- đăng nhập bằng ssh: ssh valleyDev@10.10.88.11
- khám phá chút ta được:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/2895aa3c-1d3f-460b-8699-7080f9286a66)<br>

- mật khẩu user: THM{k@l1_1n_th3_v@lley}<br>




