# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY stream-intelligence-service/pom.xml stream-intelligence-service/
RUN mvn -pl stream-intelligence-service -am dependency:go-offline
COPY stream-intelligence-service/src stream-intelligence-service/src
RUN mvn -pl stream-intelligence-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY --from=build /app/stream-intelligence-service/target/*.jar app.jar
EXPOSE 8083
ENTRYPOINT ["java", "-jar", "app.jar"]
