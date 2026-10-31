# Stage 1: Build Spring Boot application
FROM eclipse-temurin:17-jdk AS build

WORKDIR /app

COPY .mvn/ .mvn/
COPY mvnw pom.xml ./
COPY src ./src

RUN chmod +x ./mvnw && ./mvnw -B clean package -DskipTests


# Stage 2: Run Spring Boot application
FROM eclipse-temurin:17-jre

WORKDIR /app

RUN useradd --system --uid 1001 spring

COPY --from=build /app/target/*.jar app.jar

USER 1001

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]