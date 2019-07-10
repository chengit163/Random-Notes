# samba
1. 安装
```
sudo apt-get install samba
sudo apt-get autoremove samba
```
2. samba服务用户查看、添加、删除
```
sudo pdbedit -L 
sudo smbpasswd -a user  
sudo smbpasswd -x user
```
3. 配置smb.conf   
```
sudo vi /etc/samba/smb.conf
  [myshare]
	comment = myshare
	path = /home/ljc
	browseable = yes
	writable = yes
	guest ok = yes
	valid user = ljc
```
4. samba服务启动、停止、重启
```
sudo /etc/init.d/samba start
sudo /etc/init.d/samba stop
sudo /etc/init.d/smbd restart 或 sudo service smbd restart
```