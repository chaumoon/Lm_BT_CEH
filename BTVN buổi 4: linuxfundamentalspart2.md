*. task 2<br>
- truy cập vào ssh<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/ece72039-c356-4dd2-8d3b-e8e3e8fd14a9)<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/ffd2fbb6-574b-491f-ba9e-534b3c6687f3)<br>

*. task 3<br>
1. What directional arrow key would we use to navigate down the manual page?<br>
As: down<br>

2. What flag would we use to display the output in a "human-readable" way?<br>
As: -h<br>

*. task 4<br>
- touch: tạo file
- mkdir: tạo thư mục
- cp: sao chép file or thư mục
- mv: di chuyển 1 file or thư mục
- rm: xóa file or thư mục
- file: xác định loại file<br>

1. How would you create the file named "newnote"?<br>
As: touch newnote<br>

2. On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?<br>
As: ASCII text<br>

3. How would we move the file "myfile" to the directory "myfolder" <br>
As: mv myfile myfolder<br>

4. What are the contents of this file?<br>
As: THM{FILESYSTEM}<br>

*. task 5<br>
1. On the deployable machine, who is the owner of "important"?<br>
- 'ls -la':<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/8f74363e-ba7f-47b5-8102-62646dfc9e58)<br>

As: user2<br>

2. What would the command be to switch to the user "user2"?<br>
As: su user2<br>

3. Now switch to this user "user2" using the password "user2"<br>
- 'su user2' nhập passwword: user2<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/5a4dba0c-621c-4a5a-9fd9-ec913ca721d7)<br>

4. Output the contents of "important", what is the flag?<br>
As: THM{SU_USER2}<br>

*. task 6<br>
- /etc: lưu trữ các tệp hệ thống đc hđh xài (passwd, shadow, ...)
- /var (1 trong những thư mục gốc chính): lưu trữ dữ liệu thg đc truy cập or ghi bởi các dịch vụ, ứng dụng đang chạy trên hệ thống
- /root (ngôi nhà cho user root): thư mục chính cho ng dùng root, ng dùng sẽ có dữ liệu của họ trong 1 thư mục như /home/root theo mặc định
- /tmp (thư mục gốc duy nhất): ko ổn định, lưu trữ dữ liệu chỉ cần truy cập 1-2 lần; bị xóa sau khi khởi động lại; ng dùng nào cx can ghi vào thư mục này theo mặc định<br>

1. What is the directory path that would we expect logs to be stored in?<br>
As: /var/log<br>

2. What root directory is similar to how RAM on a computer works?<br>
As: /tmp<br>

3. Name the home directory of the root user <br>
As: /root<br>
