# user-registration-page
+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline - Dockerizing and Pushing to DockerHub.</br>

## Jenkins Pipeline - Dockerizing and Pushing to DockerHub.

### Prerequisites:
+ Git is installed
+ Java 17 Installed 
+ Maven is installed
+ AWS RDS MYSQL is created
+ Docker is installed
+ DockerHub repo is created

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration
 + Docker

### Step 2: Create the Docker repository
```xml
Repository Name: user-registration
```

### Step 3: Create the Jenkins Pipeline job
```xml
Job Name: pushing-docker-image-to-dockerhub-jenkins-pipeline
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/user-registration.git
Branch : pushing-docker-image-to-dockerhub-jenkinsfile
```


### Step 5: Write the Jenkinsfile
  + ### Step 5.1: Clone the repository 
```xml
stage('Clone') {
            steps {
                git branch: 'pushing-docker-image-to-dockerhub-jenkinsfile', credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }
```
  + ### Step 5.2: Build the code
```xml
stage('Build') {
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
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "/app/user-registration.jar"]
```
  + ### 6.1: Build Docker Image
```xml
stage('Build Docker Image') {
            steps {
                sh '''
               docker build . --tag user-registration:latest
               docker tag user-registration:latest mmreddy424/user-registration:latest
                
                '''
                
            }
        }
   
```
+ ###  6.2: Push Docker Image
```xml
stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
       
                    sh '''
                    docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD
                        docker push mmreddy424/user-registration:latest
                    '''
                }
            } 
            
        }
```


### Step 7: Verify whether docker image is pushed or not in DockerHub

##### Congratulations. You have successfully pushed the docker image to DockerHub using Jenkins Pipeline job.


