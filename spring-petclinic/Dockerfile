FROM java:8-alpine
VOLUME /opt/egbtm
#ADD data /
COPY target/spring-petclinic-1.5.1.jar /app/

WORKDIR /app

ENV JAVA_OPTS=""
ENTRYPOINT ["java", "-jar", "spring-petclinic-1.5.1.jar"]

