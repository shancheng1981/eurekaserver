FROM primetoninc/jdk:1.8

LABEL maintainer="shancheng1981 <19009790@qq.com>"

ADD eurekaserver-1.0.0.jar /opt/eurekaserver-1.0.0.jar

EXPOSE 9099

SHELL ["/bin/bash", "-l"]

RUN ["java", "-version"]

ENTRYPOINT ["java", "-server", "-jar", "/opt/eurekaserver-1.0.0.jar"]