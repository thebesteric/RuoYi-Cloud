FROM  openjdk:8-jdk
LABEL maintainer=eric

ENV PARAMS="--server.port=8080 --spring.profiles.active=prod --spring.cloud.nacos.config.server-addr=nacos.demo:8848 --spring.cloud.nacos.config.namespace=prod --spring.cloud.nacos.config.file-extension=yml --spring.cloud.nacos.config.username=nacos --spring.cloud.nacos.config.password=nacos --spring.cloud.nacos.discovery.server-addr=nacos.demo:8848 --spring.cloud.nacos.discovery.username=nacos --spring.cloud.nacos.discovery.password=nacos"


RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone

RUN mkdir -p /application

WORKDIR /application

COPY target/*.jar /application/app.jar

EXPOSE 8080

ENTRYPOINT ["/bin/sh","-c","java -Dfile.encoding=utf-8 -Djava.security.egd=file:/dev/./urandom -jar /application/app.jar ${PARAMS}"]