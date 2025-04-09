FROM openjdk:11 AS BUILD_IMAGE

WORKDIR /app
COPY . /app

RUN apt update && apt install -y maven \
    && mvn clean install -DskipTests

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]

