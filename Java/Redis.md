# Redis

## Linux
1. 安装
```
wget http://download.redis.io/releases/redis-3.2.13.tar.gz
tar -zxvf redis-3.2.13.tar.gz
make
sudo make install
```

2. 设置Redis自启动脚本
```
sudo cp utils/redis_init_script /etc/init.d/redisd
```
```
REDISPORT=6379
EXEC=/usr/local/bin/redis-server
CLIEXEC=/usr/local/bin/redis-cli

PIDFILE=/var/run/redis_${REDISPORT}.pid
CONF="/etc/redis/${REDISPORT}.conf"
```

2. 设置Redis配置
```
sudo mkdir /etc/redis
sudo cp redis.conf /etc/redis/6379.conf
```
sudo mkdir -p /usr/local/redis/data/db  
sudo mkdir -p /usr/local/redis/data/log  
* 设置后台运行：  
daemonize yes
* 设置log文件路径：  
logfile "/usr/local/redis/log/redis-server.log"
* 设置持久化文件存放路径：  
dir /usr/local/redis/db

3. 注册服务
```
sudo chmod +x /etc/init.d/redisd
sudo update-rc.d redisd defaults
```

4. 启动、停止、重启
```
sudo service redisd start
sudo service redisd stop
sudo service redisd restart
```

5. 问题
```
insserv: warning: script 'K01redisd' missing LSB tags and overrides
insserv: warning: script 'redisd' missing LSB tags and overrides
```
* 修改/etc/init.d/redisd:
```
#!/bin/sh
# chkconfig: 2345 10 90
# Simple Redis init.d script conceived to work on Linux systems
# as it does use of the /proc filesystem.
### BEGIN INIT INFO
# Provides:          redisd6379
# Required-Start:    $local_fs $network
# Required-Stop:     $local_fs
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: start redisd6379
# Description:       start redisd6379
### END INIT INFO
```


## Windows
https://github.com/MSOpenTech/redis/releases