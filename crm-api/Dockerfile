# New version of java base image in dockerhub:   FROM eclipse-temurin:21-jdk
FROM openjdk:21
# Set the working directory inside the container
WORKDIR /app

# Copy the source code into the container
COPY . .

# Build the application using Maven
RUN chmod +x mvnw
RUN ./mvnw package -DskipTests

# Expose the application port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "target/CRM-0.0.1-SNAPSHOT.jar"]
