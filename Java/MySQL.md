# MySQL

## Linux
sudo apt-get install mysql-server-5.7

## Windows
https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.26-winx64.zip

1. 配置环境变量
MYSQL_HOME=D:\developers\MySQL\MySQL Server 5.7
PATH=%MYSQL_HOME%\bin

2. 创建my.ini
```
[mysql]
default-character-set=utf8

[mysqld]
basedir=D:\developers\MySQL\MySQL Server 5.7
datadir=D:\developers\MySQL\MySQL Server 5.7\data
port=3306
character_set_server=utf8

[client]
port=3306
default-character-set=utf8
#sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 
#skip-grant-tables
```

3. 配置服务
* mysqld --initialize-insecure （注：生成文件夹%MYSQL_HOME%/data）
* 安装： mysqld -install / 移除： mysqld -remove
* 启动： net start MySQL / 关闭： net stop MySQL

4. 修改密码
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');