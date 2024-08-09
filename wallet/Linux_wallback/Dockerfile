#How to create jar file and dockerize a springboot application all in docker

#Stage-1
# Use a base image with JDK 11 (or another version if required)
FROM maven:3.8.5-openjdk-17 AS builder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline

COPY src/ ./src/

RUN mvn clean package -DskipTests=true


#Stage-2
FROM openjdk:11-jre-slim AS prod

WORKDIR /app

COPY --from=builder /app/target/*.jar  /app.jar

ENV SERVER_PORT=8080


EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar"]

