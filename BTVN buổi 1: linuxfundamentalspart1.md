link bài tập: https://tryhackme.com/room/linuxfundamentalspart1<br>
I. lệnh
- echo: xuất văn bản được cung cấp
- whoami: tìm xem bn đang đăng nhập vs tư cách ng dùng nào
- ls: liệt kê danh sách file, thư mục
- cd: thay đổi thư mục
- cat: đọc nội dung file
- pwd: xem thư mục đang làm việc
- find: tìm file theo các tiêu chí đc đưa ra
- grep: tìm một nội dung gì đó trong 1 file
- &; cho phép chạy lệnh trong nền của thiết bị đàu cuối
- &&: kết hợp nh lệnh lại vs nhau trong 1 dòng của thiết bị đầu cuối
- >: chuyển hướng có thay thế
- >>: chuyển hướng nma nối thêm
<br>
II. bài tập<br>
*. task 4<br>
1. If we wanted to output the text "TryHackMe", what would our command be?<br>
echo TryHackMe<br>

2. What is the username of who you're logged in as on your deployed Linux machine?<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/72bb102e-af31-4a55-84ff-47efb818adc6)<br>

tryhackme<br>

*. task 5<br>
1. On the Linux machine that you deploy, how many folders are there?<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/b6f721df-68b7-4de5-9617-9bec0acc64ad)<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/634c3050-fb3f-473f-8cfc-95cda42034d1)<br>

2. Which directory contains a file? <br>

![image](https://github.com/chaumoon/CEH/assets/127403046/e0d577d7-2e61-4fe4-8d41-e75f38ff193b)<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/3dbb5917-f12d-4613-a6cb-0450b3660314)<br>

3. What is the contents of this file?<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/a2913c76-06f5-4e4a-bc0e-bf37ec2110f9)<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/5273cff6-96e5-4c43-a8d8-e9abe4053331)<br>

4. Use the cd command to navigate to this file and find out the new current working directory. What is the path?<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/3801b2be-3d61-488a-ad16-1c076b5203c4)<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/30eb0e0c-1950-4df1-8d8a-a2532c2c380a)<br>

*. task 6<br>
1. Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag?<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/afed9cd8-7575-4c63-a989-e458a163fce4)<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/034d720a-d1b3-4c21-8ba4-1ab2e0cf9e5e)<br>

*. task 7<br>
1. If we wanted to run a command in the background, what operator would we want to use?<br>
&<br>

2. If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?<br>
echo password123 passwords<br>

3. Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be<br>
echo tryhackme >> passwords<br>
