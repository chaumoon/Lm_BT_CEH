- link bt: https://tryhackme.com/room/torforbeginners<br>

*. task 1<br>
- tor: cho phép liên lạc ẩn danh
- che giấu vị trí và cách sử dụng của ng dùng khỏi ng quản trị mạng<br>

*. task 2<br>
- https://github.com/haad/proxychains
- là công cụ buộc mọi kết nối TCP phải tuân theo proxy như torhoặc bất kỳ proxy SOCKS4, SOCKS5 hoặc HTTP(S) nào khác.
- thg xài trong giai đoạn trinh sát<br>

*. task 3<br>
- cài đặt trình duyệt tor:<br>
. https://www.torproject.org/<br>
. https://hackingpress.com/install-tor-on-kali-linux/#Step_1_Create_a_new_user<br>

. cài tor<br>
- apt-get install tor
- service tor start
- service tor status
- service tor stop
- apt install proxychains
- nano /etc/proxychains.conf (chỉnh như bên tryhackme chỉ)
- proxychains firefox
- apt install -y tor torbrowser-launcher
- mở app chạy "tor browser launcher settings" và "tor brower"
- ở "tor browser" vào mục security:<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/bd098fc6-f739-4f7e-ba23-aa91fc38302b)<br>

- chỉnh thành "safer":<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/ab5c643a-6b0b-44b5-9846-431226cad51c)<br>

- về lại trang chính và dán link vào<br>

1. Access the website below and capture the flag by copying bitcoin address at the bottom of the page!
http://danielas3rtn54uwmofdo3x2bsdifr47huasnmbgqzfrec5ubupvtpid.onion/<br>
As: 1K918TvvE4PMPzPuZT7zSDAQV4ZNUjHBm5

