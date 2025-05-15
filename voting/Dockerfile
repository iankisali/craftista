# ----------------------------------------------
# Stage 1: Build the Spring Boot application
# ----------------------------------------------

FROM maven:3.9.9-eclipse-temurin-17-alpine as build

# Set the working directory inside the container
WORKDIR /app

# Copy the project's POM file for dependency resolution
COPY pom.xml .

RUN mvn dependency:resolve

COPY src ./src

# Build the application using Maven
RUN mvn package -DskipTests

# ----------------------------------------------
# Stage 2: Create a smaller image for production
# ----------------------------------------------
FROM eclipse-temurin:17-jre-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file built in the previous stage
COPY --from=build /app/target/voting-0.0.1-SNAPSHOT.jar app.jar

# Expose port 8080 for the Spring Boot application
EXPOSE 8080

# Define the command to run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
