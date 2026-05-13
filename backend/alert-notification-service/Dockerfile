# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
COPY alert-notification-service/pom.xml alert-notification-service/
RUN mvn -pl alert-notification-service -am dependency:go-offline
COPY alert-notification-service/src alert-notification-service/src
RUN mvn -pl alert-notification-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app
COPY --from=build /app/alert-notification-service/target/*.jar app.jar
EXPOSE 8085
ENTRYPOINT ["java", "-jar", "app.jar"]
