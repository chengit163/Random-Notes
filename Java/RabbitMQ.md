# RabbitMQ 

## Linux (Ubuntu)
1. 安装erlang环境
* 在 /etc/apt/sources.list.d/ 目录下创建 bintray.erlang.list， 并加入  
deb http://dl.bintray.com/rabbitmq-erlang/debian ubuntu版本 erlang-你需要的版本
```
echo "deb http://dl.bintray.com/rabbitmq-erlang/debian xenial erlang-20.x" | sudo tee /etc/apt/sources.list.d/bintray.erlang.list
```

* ubuntu 对应版本
  * bionic for Ubuntu 18.04
  * xenial for Ubuntu 16.04
  * stretch for Debian Stretch
  * jessie for Debian Jessie

* 更新并安装
```
sudo apt-get update
sudo apt-get install erlang-nox
```

2. 安装rabbitmq-server
* 加入rabbitmq签名
```
sudo apt-key adv --keyserver "hkps.pool.sks-keyservers.net" --recv-keys "0x6B73A36E6026DFCA"
sudo wget -O - "https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc" | sudo apt-key add -
```

* 在 /etc/apt/sources.list.d/ 目录下创建 bintray.rabbitmq.list， 并加入  
deb https://dl.bintray.com/rabbitmq/debian ubuntu版本 main
```
echo "deb https://dl.bintray.com/rabbitmq/debian xenial main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
```

* 更新并安装
```
sudo apt-get update
sudo apt-get install rabbitmq-server
```

3. 启动、关闭、重启
```
sudo service rabbitmq-server start    
sudo service rabbitmq-server stop     
sudo service rabbitmq-server restart
```

* 查看rabbitmq-server状态
sudo systemctl status rabbitmq-server

4. 需要启动插件并且配置用户才能在浏览器访问可视化界面
```
# 激活插件
sudo rabbitmq-plugins enable rabbitmq_management 

# 重启
sudo service rabbitmq-server restart 

# 创建用户 sudo rabbitmqctl add_user username password
sudo rabbitmqctl add_user admin 123456 
 
# 授权管理员权限
sudo rabbitmqctl set_user_tags admin administrator
```
* http://localhost:15672