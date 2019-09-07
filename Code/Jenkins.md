# Jenkins

### 资源
* https://jenkins.io/download/
* https://jenkins.io/zh/download/
* http://mirrors.jenkins.io/war-stable/latest/jenkins.war
* http://mirrors.jenkins.io/
* http://mirrors.jenkins-ci.org/


### sonar
* Java的maven工程
```
sonar.projectKey=$JOB_NAME
sonar.projectName=$JOB_NAME
sonar.sourceEncoding=UTF-8
sonar.language=java
sonar.java.source=1.8
sonar.sources=$WORKSPACE/src
sonar.java.binaries=$WORKSPACE/target/classes/ 
```
* Android的gradle工程
```
sonar.projectKey=$JOB_NAME
sonar.projectName=$JOB_NAME
sonar.sourceEncoding=UTF-8 
sonar.language=java
sonar.java.source=1.8
sonar.java.binaries=$WORKSPACE/app/build/intermediates/classes
sonar.sources=$WORKSPACE/app/src/main/java
```
* Maven跳过测试
```
<properties>
    <maven.test.skip>true</maven.test.skip>
</properties>
```

### 插件
