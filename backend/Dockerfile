# Stage 1: Build the jar
FROM maven:3.9.4-eclipse-temurin-17 AS builder
WORKDIR /app

COPY pom.xml .
COPY mvnw .
COPY .mvn .mvn

RUN chmod +x mvnw || true
RUN ./mvnw dependency:go-offline -B

COPY src ./src
RUN ./mvnw -B package -DskipTests

# Stage 2: Run the jar
FROM eclipse-temurin:17-jre
WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
