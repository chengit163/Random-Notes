# GitLab

### 资源
* https://about.gitlab.com/downloads
* https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce
* 社区版 (gitlab-ce)
* 企业版 (gitlab-ee)

### 1. 安装
#### 安装依赖
* sudo apt-get update
* sudo apt-get install curl openssh-server ca-certificates postfix

#### apt安装
* sudo curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
* sudo apt-get install gitlab-ce
或
* sudo EXTERNAL_URL="https://gitlab.example.com" apt-get install gitlab-ce

#### dpkg安装
* sudo dpkg -i gitlab-ce_11.9.9-ce.0_amd64.deb

### 2. 启动
#### 启动sshd和postfix服务
* service sshd start
* service postfix start

#### 添加防火墙规则
* sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

#### 配置并启动GitLab
* sudo gitlab-ctl reconfigure

#### 检查GitLab是否安装好并且已经正确运行
* sudo gitlab-ctl status


### 3. 配置
#### 修改配置/etc/gitlab/gitlab.rb，GitLab显示的仓库链接
```
external_url 'http://gitlab.example.com'
```

#### 重新生成配置并启动GitLab
* gitlab-ctl reconfigure

#### 清空缓存
* gitlab-rake cache:clear RAILS_ENV=production

#### 重启所有GitLab组件
* gitlab-ctl restart


### 4. 更新
#### 当前版本
* cat /opt/gitlab/embedded/service/gitlab-rails/VERSION

#### 首次更新
* sudo touch /etc/gitlab/skip-auto-migrations

#### 更新GitLab
* gitlab-ctl stop
* sudo apt-get update && sudo apt-get install gitlab-ce

#### 重启GitLab
* sudo gitlab-ctl reconfigure
* sudo gitlab-ctl restart


### 5. 卸载
#### 停止GitLab
* sudo gitlab-ctl stop

#### 查看进程
* ps -e | grep gitlab

#### 删除所有包含gitlab的文件及目录(su)
* find / -name gitlab | xargs rm -rf

#### 卸载
* sudo apt-get remove gitlab-ce

#### 检查还有没有卸载的gitlab相关软件
* dpkg --get-selections | grep gitlab
gitlab-ce deinstall

#### 再执行
* sudo apt-get --purge remove gitlab-ce


### 6. 备份
#### 修改配置/etc/gitlab/gitlab.rb
```
gitlab_rails['manage_backup_path'] = true
gitlab_rails['backup_path'] = "/data/gitlab-backups"
gitlab_rails['backup_archive_permissions'] = 0644        //生成的备份文件权限
gitlab_rails['backup_keep_time'] = 7776000              //备份保留天数为3个月（即90天，这里是7776000秒）
```

#### 
默认 /var/opt/gitlab/backups
* sudo mkdir -p /data/gitlab-backups
* sudo chown -R git.git /data/gitlab-backups
* sudo chmod -R 777 /data/gitlab-backups
* sudo gitlab-ctl reconfigure

#### 备份
* sudo gitlab-rake gitlab:backup:create


### 7. 恢复
#### 停止相关数据连接服务
* sudo gitlab-ctl stop unicorn
* sudo gitlab-ctl stop sidekiq
* sudo gitlab-ctl status

#### 恢复
* cd /data/gitlab-backups
* sudo gitlab-rake gitlab:backup:restore BACKUP=

#### 再次启动
* sudo gitlab-ctl start