FROM openjdk:11 AS BUILD_IMAGE

WORKDIR /app

# تنظیم DNS و نصب پکیج‌ها
RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf && \
    apt-get update && \
    apt-get install -y maven && \
    apt-get clean

COPY . /app

RUN mvn clean install -DskipTests

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]


