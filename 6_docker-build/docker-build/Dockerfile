
# First stage: complete build environment
FROM maven:3.5.0-jdk-8-alpine AS builder

# add pom.xml and source code
ADD ./pom.xml pom.xml
ADD ./6_docker-build/src src/

RUN mvn clean package



FROM  java:8
#将本地文件挂载到当前容器
VOLUME   /tmp
#复制jar文件和配置文件所在的目录到容器里
ADD  my-app.jar  /app.jar
ADD  conf       /conf
#声明需要暴露的端口
EXPOSE  7070
#配置容器启动后执行的命令,并指定使用项目外部的配置文件
ENTRYPOINT  ["java","-Xms256m","-Xmx256m","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar","--spring.config.location=/conf/application.yml"]

