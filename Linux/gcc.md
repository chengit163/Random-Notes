# gcc
1. 安装
```
sudo apt-get install gcc-4.9 g++-4.9
sudo apt-get install gcc-4.9 gcc-4.9-multilib g++-4.9 g++-4.9-multilib
```
2. 查看当前安装的版本
```
ll /usr/bin/gcc*
```
3. update-alternatives设置gcc和g++的版本
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 49
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 49

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 50
```
4. 选择gcc和g++的版本
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```
5. 删除gcc和g++的版本
```
sudo update-alternatives --remove gcc /usr/bin/gcc-4.9
sudo update-alternatives --remove gcc /usr/bin/g++-4.9
apt-remove
```