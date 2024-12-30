# user-registration-page

+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Freestyle Job - Dockerizing and Pushing to AWS ECR.</br>

## Jenkins Freestyle Job - Dockerizing and Pushing to AWS ECR..

### Prerequisites:
+ Jenkins is installed
+ Git is installed
+ Java 17 Installed 
+ Maven is installed
+ AWS RDS MYSQL is created
+ Docker is installed
+ DockerHub repo is created
+ Github token generate

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration

### Step 2: Create the AWS ECR repository
```xml
Name: user-registration
```

### Step 3: Create the Jenkins Freestyle job
```xml
Job Name: pushing-docker-image-to-ecr-freestyle
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/user-registration.git
Branch : pushing-docker-image-to-ecr-freestyle
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
docker tag user-registration:latest 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
```
### Step 8: Configure the AWS credenatils in Jenkins Server or attach the IAM role to the jenkins server 
### Step 9: login to AWS ECR
```xml
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 266735810449.dkr.ecr.us-east-1.amazonaws.com
```
### Step 10: Push to AWS ECR
```xml
docker push 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
```
### Step 11: Verify whether docker image is pushed or not in AWS ECR

#### Congratulations. You have successfully Pushed the docker image to AWS ECR using Jenkins freestyle job.
