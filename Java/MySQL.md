# MySQL

### 资源
#### Linux
* sudo apt-get install mysql-server-5.7
## Windows
* https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.26-winx64.zip


### 1. 配置环境变量
```
MYSQL_HOME=D:\developers\MySQL\MySQL Server 5.7
PATH=%MYSQL_HOME%\bin
```


### 2. 创建my.ini
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


### 3. 配置服务
* mysqld --initialize-insecure （注：生成文件夹%MYSQL_HOME%/data）
* 安装： mysqld -install / 移除： mysqld -remove
* 启动： net start MySQL / 关闭： net stop MySQL


### 4. 修改密码
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');


### 5. 用户
#### 增加
```
CREATE DATABASE 数据库 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER '用户名' IDENTIFIED BY '密码';
GRANT 权限 ON 数据库.* TO '用户名'@'%' IDENTIFIED BY '密码'; 
GRANT 权限 ON 数据库.* to '用户名'@'localhost' IDENTIFIED BY '密码';
FLUSH PRIVILEGES;
```

#### 删除
```
DROP DATABASE 数据库;
DROP USER '用户名'@'%';
DROP USER '用户名'@'localhost';
FLUSH PRIVILEGES;
```


### 6. 备份
```
#!/bin/bash

#----------------------------------------------------------------
# MySQL备份脚本
#----------------------------------------------------------------
export PATH=/bin:/usr/bin:/usr/local/bin

BACKUP_PATH='/home/ljc/backups/mysql-backups'
BACKUP_TIME=`date +"%Y%m%d%H%M%S"`
BACKUP_KEEP=30
BACKUP_LOG="$BACKUP_PATH/"backup.log

DB_HOST='localhost'
DB_PORT='3306'
DB_USER='root'
DB_PASSWD='123456'
DB_NAME='mysql'


#----------------------------------------------------------------
# 备份执行
#----------------------------------------------------------------
mkdir -p ${BACKUP_PATH}

echo "$(date +'%Y-%m-%d %H:%M:%S'): [${DB_NAME}] 备份执行开始..." >> "$BACKUP_LOG"

# 如非使用InnoDB存储引擎且备份需要花费太多时间（会锁定），可删除“ --single-transaction \”参数
mysqldump \
   -h${DB_HOST} \
   -P${DB_PORT} \
   -u${DB_USER} \
   -p${DB_PASSWD} \
   --default-character-set=utf8 \
   --single-transaction \
   ${DB_NAME} | gzip > ${BACKUP_PATH}/${DB_NAME}-${BACKUP_TIME}.sql.gz
 
if [ $? -eq 0 ]; then
  echo "$(date +'%Y-%m-%d %H:%M:%S'): [${DB_NAME}] 备份执行完成..." >> "$BACKUP_LOG"
else
  echo "$(date +'%Y-%m-%d %H:%M:%S'): [${DB_NAME}] 备份执行失败..." >> "$BACKUP_LOG"
fi
 

#----------------------------------------------------------------
# 备份清理
#----------------------------------------------------------------
echo "$(date +'%Y-%m-%d %H:%M:%S'): [${DB_NAME}] 备份清理开始..." >> "$BACKUP_LOG"
find ${BACKUP_PATH} -name "${DB_NAME}-*.sql.gz" -type f -mtime +${BACKUP_KEEP} | while read line
do
    echo "删除 [$line]" >> "$BACKUP_LOG"
    rm -f $line
done
echo "$(date +'%Y-%m-%d %H:%M:%S'): [${DB_NAME}] 备份清理结束..." >> "$BACKUP_LOG"
echo " " >> "$BACKUP_LOG"
```

#### 定时
crontab -e
crontab -l
