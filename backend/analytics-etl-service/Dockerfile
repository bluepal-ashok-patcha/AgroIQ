# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY analytics-etl-service/pom.xml analytics-etl-service/
RUN mvn -pl analytics-etl-service -am dependency:go-offline
COPY analytics-etl-service/src analytics-etl-service/src
RUN mvn -pl analytics-etl-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY --from=build /app/analytics-etl-service/target/*.jar app.jar
EXPOSE 8086
ENTRYPOINT ["java", "-jar", "app.jar"]
