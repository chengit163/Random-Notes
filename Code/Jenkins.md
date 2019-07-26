# Jenkins

### sonar
```
sonar.projectKey=$JOB_NAME
sonar.projectName=$JOB_NAME
sonar.language=java
sonar.java.binaries=$WORKSPACE/target/classes/ 
sonar.sources=$WORKSPACE/src
sonar.java.source=1.8
sonar.sourceEncoding=UTF-8  
```