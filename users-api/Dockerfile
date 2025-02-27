# Build stage - multistage build
# Using maven image as build stage
FROM maven:3.8-openjdk-8 AS build
WORKDIR /app
COPY pom.xml ./
RUN mvn dependency:go-offline
COPY . .
RUN mvn package -DskipTests

# Production stage
FROM openjdk:8-jdk-slim
WORKDIR /app
COPY --from=build /app/target/users-api-0.0.1-SNAPSHOT.jar users.jar
EXPOSE 8083
CMD ["java", "-jar", "users.jar"]