# sonar

### 资源
* https://binaries.sonarsource.com/Distribution/sonarqube/ (sonarqube-6.7.7.zip)
* https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/ (sonar-scanner-cli-3.3.0.1492-linux.zip)
* https://github.com/SonarQubeCommunity/sonar-l10n-zh (中文插件)
* https://github.com/SonarOpenCommunity/sonar-cxx (C/C++插件)

### 1. 安装


### 2. 配置
``` 
CREATE DATABASE sonar DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER 'sonar' IDENTIFIED BY 'sonar';
GRANT ALL ON sonar.* TO 'sonar'@'%' IDENTIFIED BY 'sonar'; 
GRANT ALL ON sonar.* TO 'sonar'@'localhost' IDENTIFIED BY 'sonar';
FLUSH PRIVILEGES;
```

* vi SONARQUBE_HOME/conf/sonar.properties
```
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance
```

* vi SONAR_RUNNER_HOME/conf/sonar-scanner.properties
```
sonar.jdbc.username=sonar  
sonar.jdbc.password=sonar  
sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance
```


### 3. 插件
* cp xxx.jar SONAR_HOME/extensions/plugins


### 4.默认
用户名: admin
密码: admin
