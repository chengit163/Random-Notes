# GitLab
https://about.gitlab.com/downloads/  
https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/
社区版 (gitlab-ce)  
企业版 (gitlab-ee)  

1. 安装
* 安装依赖
```
sudo apt-get update
sudo apt-get install curl openssh-server ca-certificates postfix
```
* 添加仓库
```
sudo curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt-get install gitlab-ce
或
sudo EXTERNAL_URL="https://gitlab.example.com" apt-get install gitlab-ce
```

2. 启动
* 启动sshd和postfix服务
```
service sshd start
service postfix start
```
* 添加防火墙规则
```
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```
* 配置并启动GitLab
```
sudo gitlab-ctl reconfigure
```
* 检查GitLab是否安装好并且已经正确运行
```
sudo gitlab-ctl status
```

3. 配置
* 修改配置/etc/gitlab/gitlab.rb，GitLab里面显示的仓库链接
```
external_url 'http://gitlab.xxx.com'
```
* 重新生成配置，启动服务
```
gitlab-ctl reconfigure
```
* 清空缓存
```
gitlab-rake cache:clear RAILS_ENV=production
```
* 重启所有GitLab组件
```
gitlab-ctl restart
```

4. 更新
* 首次更新
```
sudo touch /etc/gitlab/skip-auto-migrations
```
* 更新GitLab
```
gitlab-ctl stop
sudo apt-get update && sudo apt-get install gitlab-ce
```
* 重启GitLab
```
sudo gitlab-ctl reconfigure
sudo gitlab-ctl restart
```

5. 卸载
```
# 停止gitlab
sudo gitlab-ctl stop

# 查看进程
ps -e | grep gitlab

# 删除所有包含gitlab的文件及目录
find / -name gitlab | xargs rm -rf

# 卸载
sudo apt-get remove gitlab-ce

# 检查还有没有卸载的gitlab相关软件
dpkg --get-selections | grep gitlab
gitlab-ce deinstall

# 再执行
sudo apt-get --purge remove gitlab-ce
```