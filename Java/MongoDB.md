# MongoDB

## Linux  
https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.13.tgz

1. 配置环境变量
* sudo tar -zxvf mongodb-linux-x86_64-3.6.12.tgz
* sudo mv mongodb-linux-x86_64-3.6.12 /usr/local/mongodb
* export MONGODB_HOME=/usr/local/mongodb

2. 配置MongoDB服务
sudo mkdir -p /usr/local/mongodb/data/db
sudo mkdir -p /usr/local/mongodb/data/log
```
dbpath=/usr/local/mongodb/data/db
logpath=/usr/local/mongodb/data/log/mongodb.log
logappend=true
journal=true
quiet=true
port=27017
fork=true #后台运行
bind_ip=0.0.0.0 #允许任何IP进行连接
auth=false #是否授权连接
```

3. 配置MongoDB启动
* sudo vi /lib/systemd/system/mongodb.service
```
[Unit]  
Description=mongodb  
After=network.target remote-fs.target nss-lookup.target  
  
[Service]  
Type=forking  
ExecStart=/usr/local/mongodb/bin/mongod --config /etc/mongodb.conf  
ExecReload=/bin/kill -s HUP $MAINPID  
ExecStop=/usr/local/mongodb/bin/mongod --shutdown --config /etc/mongodb.conf  
PrivateTmp=true  
  
[Install]  
WantedBy=multi-user.target
```
* sudo chmod 754 /lib/systemd/system/mongodb.service
* 启动服务  
systemctl start mongodb.service  
* 关闭服务  
systemctl stop mongodb.service  
* 重启服务
systemctl restart mongodb.service  
* 开启开机启动  
systemctl enable mongodb.service  
* 禁用开机启动
systemctl disable mongodb.service  


## Windows 
http://downloads.mongodb.org/win32/mongodb-win32-x86_64-2008plus-ssl-3.6.12.zip

1. 配置环境变量  
* MONGODB_HOME=D:\developers\MongoDB\mongodb-3.6.12
* PATH=%MONGODB_HOME%\bin
* mongod --version

2. 运行MongoDB服务
* mongod --dbpath D:\developers\MongoDB\mongodb-3.6.12\data\db

3. 配置MongoDB服务
* 创建一个配置文件位于 D:\developers\MongoDB\mongodb-3.6.12\mongod.cfg，其中指定 systemLog.path 和 storage.dbPath。具体配置内容如下：
```
systemLog:
    destination: file
    path: D:\developers\MongoDB\mongodb-3.6.12\data\log\mongodb.log
    logAppend: true
storage:
    journal:
        enabled: true
    dbPath: D:\developers\MongoDB\mongodb-3.6.12\data\db
net:
    port: 27017
```
* 安装MongoDB服务  
mongod --config "D:\developers\MongoDB\mongodb-3.6.12\mongod.cfg" --install

* 移除MongoDB服务  
mongod --remove

4. 启动、关闭MongoDB服务  
net start MongoDB  
net stop MongoDB  

