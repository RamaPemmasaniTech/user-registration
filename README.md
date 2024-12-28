+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for the Jenkins Pipeline to build the application and generate the jar file</br>

## Jenkins Pipeline - Build the application

### Prerequisites:
+ Git is installed
+ Java 17 Installed 
+ Maven is installed
+ AWS RDS MYSQL is created

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  
### Step 2: Create the Jenkins Pipeline job under user-management folder
```xml
Job Name: build-pipeline
```
### Step 3: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/user-registration.git
Branch : build-jenkinsfile
```
### Step 4: Write the Jenkinsfile
  + ### Step 4.1: Clone the repository 
```xml
stage('Clone the Repository ') {
            steps {
               git branch: 'build-jenkinsfile', credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
               
               
            }
        }
```
  + ### Step 4.2: Build the code
```xml
stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
```

### Step 5: Verify whether the artifact (jar) is generated or not

#### Congratulations! You have successfully generated the artifact (Jar) file using the Jenkins Pipeline job.

