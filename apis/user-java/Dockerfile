# First stage to build the application
FROM maven:3.5.4-jdk-11-slim AS build-env

ADD apis/user-java/pom.xml pom.xml
ADD apis/user-java/src src/
RUN mvn clean package

# build runtime_ image
FROM openjdk:11-jre-slim

EXPOSE 8080

ENV SQL_USER="demousersa" \
SQL_PASSWORD="demo@pass123" \
SQL_SERVER="openhack06u2z0e9sql.database.windows.net" \
SQL_DBNAME="mydrivingDB"

# Add the application's jar to the container
COPY --from=build-env target/swagger-spring-1.0.0.jar user-java.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/user-java.jar"]
