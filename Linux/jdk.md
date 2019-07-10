# jdk
1. 安装
```
sudo mkdir /usr/lib/java
sudo tar -zxvf jdk-8u181-linux-x64.tar.gz -C /usr/lib/java
```
2. 修改环境变量
```
vim /etc/profile
source /etc/profile
# set orable jdk
export JAVA_HOME=/user/lib/java/jdk1.8.0_181
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin
```
3. 设置默认jdk
```
sudo update-alternatives --install /usr/bin/java java /usr/lib/java/jdk1.8.0_181/bin/java 300
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/java/jdk1.8.0_181/bin/javac 300
sudo update-alternatives --install /usr/bin/jar jar /usr/lib/java/jdk1.8.0_181/bin/jar 300
sudo update-alternatives --install /usr/bin/javah javah /usr/lib/java/jdk1.8.0_181/bin/javah 300
sudo update-alternatives --install /usr/bin/javap javap /usr/lib/java/jdk1.8.0_181/bin/javap 300
```
4. 选择jdk版本
```
sudo update-alternatives --config java
```
5. 查看jdk版本
```
java -version
javac -version
```