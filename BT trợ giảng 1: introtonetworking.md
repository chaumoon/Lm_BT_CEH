- link bt: https://tryhackme.com/room/introtonetworking<br>

*. task 2<br>
1. Which layer would choose to send data over TCP or UDP?<br>
As: 4<br>

2. Which layer checks received information to make sure that it hasn't been corrupted?<br>
As: 2<br>

3. In which layer would data be formatted in preparation for transmission?<br>
As: 2<br>

4. Which layer transmits and receives data?<br>
As: 1<br>

5. Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format?<br>
As: 6<br>

6. Which layer tracks communications between the host and receiving computers?<br>
As: 5<br>

7. Which layer accepts communication requests from applications?<br>
As: 7<br>

8. Which layer handles logical addressing?<br>
As: 3<br>

9. When sending data over TCP, what would you call the "bite-sized" pieces of data?<br>
As: segments<br>

10. [Research] Which layer would the FTP protocol communicate with?<br>
As: 7<br>

11. Which transport layer protocol would be best suited to transmit a live video?<br>
As: udp<br>

*. task 3<br>
1. How would you refer to data at layer 2 of the encapsulation process (with the OSI model)?<br>
As: frames<br>

2. How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected?<br>
As: datagrams<br>

3. What process would a computer perform on a received message?<br>
As: de-encapsulation<br>

4. Which is the only layer of the OSI model to add a trailer during encapsulation?<br>
As: data link<br>

5. Does encapsulation provide an extra layer of security (Aye/Nay)?<br>
As: aye<br>

*. task 4<br>
1. Which model was introduced first, OSI or TCP/IP?<br>
As: TCP/IP<br>

2. Which layer of the TCP/IP model covers the functionality of the Transport layer of the OSI model (Full Name)?<br>
As: transport<br>

3. Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model (Full Name)?<br>
As: application<br>

4. The Network Interface layer of the TCP/IP model covers the functionality of two layers in the OSI model. These layers are Data Link, and?.. (Full Name)?<br>
As: physical <br>

5. Which layer of the TCP/IP model handles the functionality of the OSI network layer?<br>
As: internet<br>

6. What kind of protocol is TCP?<br>
As: connection-based<br>

7. What is SYN short for?<br>
As: synchronise<br>

8. What is the second step of the three way handshake?<br>
As: syn/ack<br>

9. What is the short name for the "Acknowledgement" segment in the three-way handshake?<br>
As: ack<br>

*. task 5<br>
1. What command would you use to ping the bbc.co.uk website?<br>
As: ping bbc.co.uk<br>

2. What is the IPv4 address?<br>
- nhập lệnh: nslookup -type=A muirlandoracle.co.uk<br>

![image](https://github.com/chaumoon/Lm_BT_CEH/assets/127403046/1fb57204-b59e-4b9c-ac6e-b2e8c828c37e)<br>

As: 217.160.0.152<br>

3. What switch lets you change the interval of sent ping requests?<br>
As: -i<br>

4. What switch would allow you to restrict requests to IPv4?<br>
As: -4<br>

5. What switch would give you a more verbose output?<br>
As: -v<br>

*. task 6<br>
1. What switch would you use to specify an interface when using Traceroute?<br>
As: -i<br>

2. What switch would you use if you wanted to use TCP SYN requests when tracing the route?<br>
As: -T<br>

3. [Lateral Thinking] Which layer of the TCP/IP model will traceroute run on by default (Windows)?<br>
As: internet<br>

*. task 7<br>
1. What is the registrant postal code for facebook.com?<br>
As: 94025<br>

2. When was the facebook.com domain first registered (Format: DD/MM/YYYY)?<br>
As: 29/03/1997<br>

3. Which city is the registrant based in?<br>
As: Redmond<br>

4. [OSINT] What is the name of the golf course that is near the registrant address for microsoft.com?<br>
As: Bellevue Golf Course<br>

5. What is the registered Tech Email for microsoft.com?<br>
As: msnhst@microsoft.com<br>

*. task 8<br>
1. What is DNS short for?<br>
As: Domain Name System<br>

2. What is the first type of DNS server your computer would query when you search for a domain?<br>
As: recursive<br>

3. What type of DNS server contains records specific to domain extensions (i.e. .com, .co.uk*, etc)*? Use the long version of the name.<br>
As: Top-Level Domain <br>

4. Where is the very first place your computer would look to find the IP address of a domain?<br>
As: local cache<br>

5. [Research] Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one?<br>
As: 8.8.4.4<br>

6. If a DNS query has a TTL of 24 hours, what number would the dig query show?<br>
- tính bằng giây -> 24*3600<br>

As: 86400<br>
