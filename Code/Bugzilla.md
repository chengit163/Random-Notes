# Bugzilla

### 资源
* https://ftp.mozilla.org/pub/webtools/
* https://github.com/repeat/bugzilla-tw/

### 1. 安装
* sudo apt-get install apache2
* sudo apt-get install mysql-server
* sudo apt-get install libdbd-mysql-perl

* cd /var/www/html/bugzilla
* sudo perl checksetup.pl
* sudo perl install-module.pl --all

### 2. 配置
```
CREATE DATABASE bugs DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER 'bugs' IDENTIFIED BY 'bugs';
GRANT ALL ON bugs.* TO 'bugs'@'%' IDENTIFIED BY 'bugs'; 
GRANT ALL ON bugs.* TO 'bugs'@'localhost' IDENTIFIED BY 'bugs';
FLUSH PRIVILEGES;
```

* sudo vi /var/www/html/bugzilla/localconfig
```
$db_driver = 'mysql';
$db_host = 'localhost';
$db_name = 'bugs';
$db_user = 'bugs';
$db_pass = 'bugs';
$db_port = 3306; 
$index_html = 1;
```

### 3. 服务
* sudo vi /etc/apache2/sites-available/bugzilla.conf
```
<Directory /var/www/html/bugzilla>
  AddHandler cgi-script .cgi
  Options +ExecCGI
  DirectoryIndex index.cgi index.html
  AllowOverride All
</Directory>
```
* sudo a2ensite bugzilla
* sudo a2enmod cgi headers expires 
* sudo service apache2 restart