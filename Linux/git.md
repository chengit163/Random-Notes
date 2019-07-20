# git

1. 安装
```
sudo apt-get install git
```

2. 创建git用户
```
sudo adduser git   
su git
mkdir /home/git/.ssh
chmod 700 /home/git/.ssh
touch /home/git/.ssh/authorized_keys
chmod 600 /home/git/.ssh/authorized_keys
```
* 禁止git用户ssh登录
```
sudo vi /etc/passwd
git:x:1000:1000::/home/git:/usr/bin/git-shell
```
* sudo vi /etc/ssh/sshd_config
```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
* 重启sshd
systemctl stop sshd.service
systemctl start sshd.service

3. 初始化仓库
```
mkdir repository
cd repository
git init --bare project.git
chown -R git.git project.git
```

4. 克隆
git clone git@ip:/home/git/repository/project.git