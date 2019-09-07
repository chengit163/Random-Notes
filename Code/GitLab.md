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

* 默认 /var/opt/gitlab/backups
* sudo mkdir -p /data/gitlab-backups
* sudo chown -R git.git /data/gitlab-backups
* sudo chmod -R 777 /data/gitlab-backups
* sudo gitlab-ctl reconfigure

#### 备份
* sudo gitlab-rake gitlab:backup:create

#### 自动
* 编写备份脚本，结合crontab实施自动定时备份，比如每天0点、6点、12点、18点各备份一次
* 注意：环境变量CRON=1的作用是如果没有任何错误发生时， 抑制备份脚本的所有进度输出
* vi /data/gitlab/backups/gitlab_backup.sh
```
#!/bin/bash
/usr/bin/gitlab-rake gitlab:backup:create CRON=1
```
* crontab -l
```
0 0,6,12,18 * * * /bin/bash -x /data/gitlab/backups/gitlab_backup.sh > /dev/null 2>&1
```

### 7. 恢复
#### 停止相关数据连接服务
* sudo gitlab-ctl stop unicorn
* sudo gitlab-ctl stop sidekiq
* sudo gitlab-ctl status

#### 恢复
* cd /data/gitlab-backups
* sudo gitlab-rake gitlab:backup:restore BACKUP=

#### 再次启动
* sudo gitlab-ctl start unicorn
* sudo gitlab-ctl start sidekiq
* sudo gitlab-ctl start


### 7. 汉化
#### 汉化包
* https://gitlab.com/xhang/gitlab
* https://gitlab.com/xhang/gitlab/-/archive/11-11-stable-zh/gitlab-11-11-stable-zh.tar.gz
* sudo gitlab-ctl stop

#### 备份
* sudo cp -rp /opt/gitlab/embedded/service/gitlab-rails{,.bak_$(date +%F)}

#### 覆盖
* sudo cp -rf gitlab-11-11-stable-zh/* /opt/gitlab/embedded/service/gitlab-rails/

#### 重启
* sudo gitlab-ctl reconfigure
* sudo gitlab-ctl restart

#### 或者
```
git clone https://gitlab.com/xhang/gitlab.git
cd gitlab
git fetch
git diff origin/11-11-stable-stable origin/11-11-stable-stable-zh > /tmp/11-11.diff
sudo gitlab-ctl stop
cd /opt/gitlab/embedded/service/gitlab-rails
git apply /tmp/11-11.diff
or
cd /tmp
patch -d /opt/gitlab/embedded/service/gitlab-rails -p1 < 11-11.diff
```