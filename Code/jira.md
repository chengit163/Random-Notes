# jira

1. 下载
* wget https://downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.8.1-x64.bin
* wget https://downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.12.1-x64.bin
* wget https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.8.1.tar.gz
* wget https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.12.1.tar.gz

* wget http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.42/mysql-connector-java-5.1.42.jar

```
mysql-connector-java-5.1.42.jar
atlassian-extras-3.2.jar
/opt/atlassian/jira/atlassian-jira/WEB-INF/lib/
```

``` 
CREATE DATABASE sonar DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER 'jira' IDENTIFIED BY 'jira';
GRANT ALL ON jira.* TO 'jira'@'%' IDENTIFIED BY 'jira'; 
GRANT ALL ON jira.* TO 'jira'@'localhost' IDENTIFIED BY 'jira';
FLUSH PRIVILEGES;

create database jira default character set utf8 collate utf8_bin;
```