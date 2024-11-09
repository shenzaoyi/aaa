## sed grep awk

## systemctl
### ssh
```bash
sudo apt install openssh-server
sudo apt install openssh-client
sudo systemctl status ssh // 查看ssh状态
sudo systemctl start ssh // 开启ssh
```
## install
一般安装使用apt install
下载的.deb后缀文件使用
```bash
sudo dpkg -i path
```

 telnet smtp.qq.com 587
Trying 183.47.101.192...
Connected to smtp.qq.com.
Escape character is '^]'.
220 newxmesmtplogicsvrszc16-0.qq.com XMail Esmtp QQ Mail Server.
helo a
250-newxmesmtplogicsvrszc16-0.qq.com-21.34.78.104-70159832
250-SIZE 73400320
250 OK
auth login
334 VXNlcm5hbWU6
OTU0MjMzMDE0QHFxLmNvbQ==
334 UGFzc3dvcmQ6
Y2l1a3dvcGRrdmt4YmRkZQ==
530 Login fail. A secure connection is requiered(such as ssl). More information at http://service.mail.qq.com/cgi-bin/help?id=28
Connection closed by foreign host.