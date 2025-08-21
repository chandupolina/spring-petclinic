# Stage 1: Build the application
FROM maven:3.6.3-openjdk-21 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests




# Stage 2: Create the runtime image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/spring-petclinic-3.5.0-SNAPSHOT.jar   .

# Add the user to run the application
RUN useradd -ms /bin/bash chandu

# Switch to the non-root user
USER chandu

# Expose the Application
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "spring-petclinic-3.5.0-SNAPSHOT.jar"]
