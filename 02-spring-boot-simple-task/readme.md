# Simple Spring Task

Run `SpringSimpleTaskApplication` as a Java Application.

Runs `TaskImpl.performTask()` at launch

### Creating Containers

- mvn clean package
- docker run gspear/aws-simple-spring-task:0.0.1-SNAPSHOT

```
docker login
docker push gspear/aws-simple-spring-task:0.0.1-SNAPSHOT
```