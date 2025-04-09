FROM openjdk:11 AS BUILD_IMAGE

ARG SKIP_CLONE=false

RUN apt update && apt install maven -y

WORKDIR /app


RUN if [ "$SKIP_CLONE" = "false" ]; then \
    git clone https://github.com/nedakhodabakhshi/vprofile-project.git && \
    cd vprofile-project && \
    git checkout docker && \
    mvn install; \
    fi

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*


COPY --from=BUILD_IMAGE /app/vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
