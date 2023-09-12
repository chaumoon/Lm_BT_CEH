- link bt: https://tryhackme.com/room/pwnkit<br>

*. task 1<br>
- CVE-2021-4034: (Pwnkit) là lỗ hổng nâng cao đặc quyền cục bộ, nằm trong gói 'Polkit' đc cài đặt mặc định trên hầu hết hđh linux<br>

*. task 2<br>
- lỗ hổng này cho phép bất kì kẻ tấn công ko có đặc quyền nào dễ dàng có đc quyền truy cập quản trị đầy đủ đối vs máy linux cài đặt gói Polkit
- nó ko thể khai thác từ xa -> lỗ hổng leo thang đặc quyền cục bộ
- lỗ hổng tồn tại trong tiệ ích pkexec<br>

1. Is Pwnkit exploitable remotely (Aye/Nay)?<br>
As: Nay<br>

2. In which Polkit utility does the Pwnkit vulnerability reside?<br>
As: pkexec<br>

*. task 3<br>
1. What is the flag located at /root/flag.txt?<br>
As: THM{CONGRATULATIONS-YOU-EXPLOITED-PWNKIT}<br>

*. task 4<br>
