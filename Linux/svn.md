# svn
1. 
* 创建home下的svn文件夹  
sudo mkdir /home/svn
* 创建svn下的repository文件夹  
sudo mkdir /home/svn/repository
* 更改repository的权限（第一次搭建没有赋予权限，客户端访问服务器被拒绝）  
sudo chmod -R 777 /home/svn/repository
* 创建版本库  
sudo svnadmin create /home/svn/repository
* 完成后会在repository文件夹下生成以下文件  
conf、db、format、hooks、locks
* 然后对db进行权限设置  
sudo chmod -R 777 /home/svn/repository/db

2. 
* sudo vim /home/svn/repository/conf/svnserve.conf
```
[general]
anon-access = none                      # 使非授权用户无法访问
auth-access = write                     # 使授权用户有写权限
password-db = password                  # 用户密码文件
authz-db = authz                        # 访问控制文件
# realm = /home/svn/repository/         # 认证命名空间
```

* sudo vim /home/svn/repository/conf/passwd 
```
svnser = 123456
```
* sudo vim /home/svn/repository/conf/authz
```
[/]
svnuser = rw
```
```
sudo svnserve -d -r /home/svn
```