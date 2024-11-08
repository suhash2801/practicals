# Step 1: Use an official Maven image as a base image (with JDK)
FROM maven:3.8.6-openjdk-11 AS build

# Step 2: Set the working directory inside the container to /app
WORKDIR /app

# Step 3: Copy the Maven project files (pom.xml and src) into the container
COPY pom.xml .
COPY src ./src

# Step 4: Run Maven to download dependencies and build the project
# This will not skip tests; remove `-DskipTests` if you want to run tests
RUN mvn clean install

# Step 5: Set up a runtime environment using a slim OpenJDK image
FROM openjdk:11-jre-slim

# Step 6: Set the working directory for the runtime container
WORKDIR /app

# Step 7: Copy the jar file (built from the `build` stage) into the final image
COPY --from=build /app/target/simple-java-project-1.0-SNAPSHOT.jar ./simple-java-project.jar

# Step 8: The default command to run the jar file when the container starts
ENTRYPOINT ["java", "-jar", "simple-java-project.jar"]

# Expose port (optional, if your app uses a port like 8080 for web applications)
EXPOSE 8080
