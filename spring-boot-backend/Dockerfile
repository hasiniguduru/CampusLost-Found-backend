# ============================================================================
# Stage 1: Build the Spring Boot JAR using Maven and Java 21
# ============================================================================
FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /app

# Copy Maven configuration and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code and build production JAR
COPY src ./src
RUN mvn clean package -DskipTests -B

# ============================================================================
# Stage 2: Run the application on lightweight Java 21 JRE (Render Ready)
# ============================================================================
FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=build /app/target/veritas-lost-found-api-1.0.0.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
