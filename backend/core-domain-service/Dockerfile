# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY core-domain-service/pom.xml core-domain-service/
RUN mvn -pl core-domain-service -am dependency:go-offline
COPY core-domain-service/src core-domain-service/src
RUN mvn -pl core-domain-service package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY --from=build /app/core-domain-service/target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
