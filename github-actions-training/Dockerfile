# Stage 1: Build the application
FROM gradle:7.5-jdk11 AS builder

# Set the working directory
WORKDIR /app

# Copy the Gradle wrapper and build files
COPY gradlew .
COPY gradle/ gradle/
COPY build.gradle .
COPY settings.gradle .

# Copy the source code
COPY src/ src/

# Build the application
RUN ./gradlew clean build -x test

# Stage 2: Create the final image
FROM openjdk:11-jre-slim

# Set the working directory in the final image
WORKDIR /app

# Copy the built JAR file from the builder stage
COPY --from=builder /app/build/libs/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
