# Nginx

## Linux
1. 安装gcc g++的依赖库
```
sudo apt-get install build-essential
sudo apt-get install libtool
```

2. 安装pcre依赖库
```
sudo apt-get install libpcre3 libpcre3-dev
```

3. 安装zlib依赖库
```
sudo apt-get install zlib1g-dev
```

4. 安装ssl依赖库
```
sudo apt-get install openssl
```

5. 安装nginx
* wget http://nginx.org/download/nginx-1.17.1.tar.gz
```
./configure
make
sudo make install
```
6. 启动nginx：
* sudo /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
* 注意：-c 指定配置文件的路径，不加的话，nginx会自动加载默认路径的配置文件，可以通过 -h查看帮助命令。

7. 查看nginx进程：
* ps -ef | grep nginx

```
        location / {
            root   html;
            index  index.html index.htm;
	    proxy_pass http://tomcat_server;
	    proxy_redirect default;
     	    proxy_set_header Host $host;
      	    proxy_set_header X-Real-IP $remote_addr;
        }
```