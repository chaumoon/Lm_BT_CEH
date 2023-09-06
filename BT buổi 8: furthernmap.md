- link bt: https://tryhackme.com/room/furthernmap<br>

*. task 2<br>
- việc đầu tiên cần lm là quét cổng
- mỗi mt có tổng cộng 65535 cổng khả dụng<br>

. một số cổng tiru chuẩn:<br>
- http: 80
- https: 443
- windows NETBIOS: 139
- SMB: 445<br>

1. What networking constructs are used to direct traffic to the right application on a server?<br>
As: ports<br>

2. How many of these are available on any network-enabled computer?<br>
As: 65535<br>

3. [Research] How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task)<br>
As: 1024<br>

*. task 3<br>
- xài lệnh: nmap -h<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/d7a82f5a-4fc6-4117-895e-2bde30e6be2b)<br>

1. What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?<br>
As: -sS<br>

2. Which switch would you use for a "UDP scan"?<br>
As: -sU<br>

3. If you wanted to detect which operating system the target is running on, which switch would you use?<br>
As: -O<br>

4. Nmap provides a switch to detect the version of the services running on the target. What is this switch?<br>
As: -sV<br>

5. The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?<br>
As: -v<br>

6. Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?
(Note: it's highly advisable to always use at least this option)<br>
As: -vv<br>

7. What switch would you use to save the nmap results in three major formats?<br>
As: -oA<br>

8. What switch would you use to save the nmap results in a "normal" format?<br>
As: -oN<br>

9. A very useful output format: how would you save results in a "grepable" format?<br>
As: -oG<br>

10. Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning. How would you activate this setting?<br>
As: -A<br>

11. Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!
How would you set the timing template to level 5?<br>
As: -T5<br>

12. How would you tell nmap to only scan port 80?<br>
As: -p 80<br>

13. How would you tell nmap to scan ports 1000-1500?<br>
As: -p 1000-1500<br>

14. How would you tell nmap to scan all ports?<br>
As: -p-<br>

15. How would you activate a script from the nmap scripting library (lots more on this later!)?<br>
As: --script<br>

16. How would you activate all of the scripts in the "vuln" category?<br>
As: --script=vuln<br>

*. 
