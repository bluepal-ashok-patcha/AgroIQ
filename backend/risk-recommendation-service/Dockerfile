# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY risk-recommendation-service/pom.xml risk-recommendation-service/
RUN mvn -pl risk-recommendation-service -am dependency:go-offline
COPY risk-recommendation-service/src risk-recommendation-service/src
RUN mvn -pl risk-recommendation-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY --from=build /app/risk-recommendation-service/target/*.jar app.jar
EXPOSE 8084
ENTRYPOINT ["java", "-jar", "app.jar"]
