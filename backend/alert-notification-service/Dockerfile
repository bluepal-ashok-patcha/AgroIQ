# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY discovery-service/pom.xml discovery-service/
COPY api-gateway-service/pom.xml api-gateway-service/
COPY core-domain-service/pom.xml core-domain-service/
COPY ingestion-service/pom.xml ingestion-service/
COPY stream-intelligence-service/pom.xml stream-intelligence-service/
COPY risk-recommendation-service/pom.xml risk-recommendation-service/
COPY alert-notification-service/pom.xml alert-notification-service/
COPY analytics-etl-service/pom.xml analytics-etl-service/

RUN mvn -pl alert-notification-service -am dependency:go-offline
COPY alert-notification-service/src alert-notification-service/src
RUN mvn -pl alert-notification-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY --from=build /app/alert-notification-service/target/*.jar app.jar
EXPOSE 8085
ENTRYPOINT ["java", "-jar", "app.jar"]
