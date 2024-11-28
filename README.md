# user-registration-page
+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline Job - Dockerizing and Pushing to AWS ECR.</br>

## Jenkins Pipeline Job - Dockerizing and Pushing to AWS ECR..

### Prerequisites:
+ Jenkins is installed
+ Docker is installed
+ AWS cli is installed
+ Github token generate

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration

### Step 2: Create the AWS ECR repository
```xml
Name: user-registration
```

### Step 3: Create the Jenkins Pipeline job
```xml
Job Name: pushing-docker-image-to-ecr-jenkins-pipeline
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/user-registration.git
Branch : pushing-docker-image-to-ecr-jenkinsfile
```

### Step 5: Write the Jenkinsfile
  + ### Step 5.1: Clone the repository 
```xml
stage('Clone the repository') {
            steps {
               git branch: 'pushing-docker-image-to-ecr-jenkinsfile', credentialsId: 'github-credentials', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }
```
  + ### Step 5.2: Build the code
```xml
stage('Build the application') {
            steps {
                sh 'mvn clean package'
            }
        }
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
EXPOSE 80

# Command to run the application
CMD ["java", "-jar", "/app/user-registration.jar"]

```
  + ### 6.1: Build Docker Image
```xml
stage('Build Docker Image') {
            steps {
                sh '''
              docker build . --tag user-registration:latest
              docker tag user-registration:latest 533267221649.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
                
                '''
                
            }
        }
   
```
+ ### 6.2: Push Docker Image to AWS ECR

```xml
stage('Push Docker Image to AWS ECR') {
steps{
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 533267221649.dkr.ecr.us-east-1.amazonaws.com
                   docker push 533267221649.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
                    '''
            } 

        }
```


### Step 7: Verify whether docker image is pushed or not in AWS ECR

#### Congratulations. You have successfully Pushed the docker image to AWS ECR using Jenkins Pipeline job.

