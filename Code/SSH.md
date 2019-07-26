# SSH

### 1. 生成
* cd ~/.ssh
* ssh-keygen -t rsa -C "cheng_it@163.com"
* ssh-keygen -t rsa -C "lujiancheng@gitlab.com"


### 2. 添加
* ssh-agent -s
* ps aux | grep ssh
* exec ssh-agent bash
* eval ssh-agent -s
* ssh-add ./id_rsa_github
* ssh-add ./id_rsa_gitlab


### 3. 配置
* touch ~/.ssh/config
```
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_github
User chengit163

# gitlab
Host gitlab.example.com
HostName gitlab.example.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_gitlab
User lujiancheng
```


### 4. 测试
* ssh -T git@github.com          #测试github
* ssh -T git@gitlab.example.com  #测试gitlab