link bài tập: https://tryhackme.com/room/linuxprivesc<br>
*. task 1<br>
- kết nối ssh: ssh user@10.10.234.217 -oHostKeyAlgorithms=+ssh-rsa<br>

1. Run the "id" command. What is the result?<br>
As: uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)<br>

*. task 3<br>
- đọc file shadow<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/b0ca1430-6a96-40f5-b6b1-100c150ea0e2)<br>

- tạo file hash.txt<br>
chữa sau<br>

*. task 5<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/c080e56d-ee68-4f03-89d0-582c87c83503)<br>

As: uid=0(root) gid=0(root) groups=0(root)<br>

*. task 6<br>
1. How many programs is "user" allowed to run via sudo? <br>
- chạy: sudo -l<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/047e6029-d5aa-4660-80a7-d32d7e4f1067)<br>

As: 11<br>

2. One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?<br>
As: apache2<br>

*. task 9<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/1f8f3ce5-6dce-4af2-90bf-e23204a0fdd5)<br>

As: /home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin<br>

*. task 16<br>
1. What is the full mysql command the user executed?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/9dbb46cc-817d-4691-8ed9-559c83909479)<br>

As: mysql -h somehost.local -uroot -ppassword123<br>

*. task 17<br>
1. What file did you find the root user's credentials in?<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/ec7ca139-00fb-4983-b713-1fd42b79b313)<br>

As: /etc/openvpn/auth.txt<br>

*. task 19<br>
1. What is the name of the option that disables root squashing?<br>
As: no_root_squash
