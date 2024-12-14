# user-registration
+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b>Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for manually Dockerizing and Pushing to DockerHub.</br>

## Manually - Dockerizing and Pushing to DockerHub

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ DockerHub repository is created
+ AWS RDS MYSQL is created


### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/user-registration.git
  Branch Name: pushing-docker-image-to-dockerhub
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the repository in DockerHub
```xml
Repository Name: user-registration
```
### Step 4: Write the Dockerfile
```xml
# Use an OpenJDK base image
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the target directory
COPY target/*.jar /app/user-registration.jar

# Expose the application's port (update if your application uses a specific port)
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "/app/user-registration.jar"]

```
### Step 5: Build and tag the Docker image
```xml
docker build . --tag user-registration:latest
docker tag user-registration:latest mmreddy424/user-registration:latest
```
### Step 6: Login to DockerHub in local
```xml
docker login -u your-username -p your-password
```
### Step 7: Push the docker image to DockerHub
```xml
docker push mmreddy424/user-registration:latest
```
### Step 8: Verify whether docker image is pushed or not in DockerHub

#### Congratulations. You have successfully pushed the docker image to DockerHub.
