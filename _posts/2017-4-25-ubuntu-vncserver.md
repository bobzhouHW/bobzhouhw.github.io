---
layout: post
title: Ubuntu 16.04 vncserver 安装
---

安装 X11VNC
---
sudo apt install x11vnc -y


配置访问密码
---
sudo x11vnc -storepasswd /etc/x11vnc.pass 

创建服务
---
vi  /lib/systemd/system/x11vnc.service

**粘贴如下代码，最后 :wq 保存，请使用root用户，否则没有权限。**

[Unit]  
Description=Start x11vnc at startup.  
After=multi-user.target  
[Service]  
Type=simple  
ExecStart=/usr/bin/x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /etc/x11vnc.pass -rfbport 5900 -shared  
[Install]  
WantedBy=multi-user.target  

配置防火墙，配置和启动服务
---
sudo ufw allow 5900  
sudo systemctl enable x11vnc.service  
sudo systemctl daemon-reload  

参考文献
---
http://blog.csdn.net/longhr/article/details/51657610