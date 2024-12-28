# user-registration-page
+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Freestyle - Dockerizing and Pushing to DockerHub.</br>

## Jenkins Freestyle - Dockerizing and Pushing to DockerHub.

### Prerequisites:
+ Jenkins is installed
+  Docker is installed
+  Github token generate

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration

### Step 2: Create the Docker repository
```xml
Name: user-registration
```

### Step 3: Create the Jenkins Freestyle job
```xml
Job Name: pushing-docker-image-to-dockerhub-freestyle
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/user-registration.git
Branch : pushing-docker-image-to-dockerhub-freestyle
```
### Step 5: Invoke the top level maven targets
```xml
clean package
```
### Step 6: Write the Dockerfile
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
### Step 7: Build and tag the Docker image
```xml
docker build . --tag user-registration:latest
docker tag user-registration:latest mmreddy424/user-registration:latest
```
### Step 8: login to DockerHub
```xml
docker login -u mmreddy424 -p Docker@2580
```
### Step 9: Push to DockerHub
```xml
docker push mmreddy424/user-registration:latest
```
### Step 10: Verify whether docker image is pushed or not in DockerHub

##### Congratulations. You have successfully pushed the docker image to DockerHub using Jenkins freestyle job.

