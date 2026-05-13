# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
COPY ingestion-service/pom.xml ingestion-service/
RUN mvn -pl ingestion-service -am dependency:go-offline
COPY ingestion-service/src ingestion-service/src
RUN mvn -pl ingestion-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app
COPY --from=build /app/ingestion-service/target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]
