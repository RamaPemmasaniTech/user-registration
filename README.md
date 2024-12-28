+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b> Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for manually building the application and generating the Jar file using Jenkins Freestyle jobs</br>

## using Jenkins Freestyle  - building the application and generating the Jar file

### Prerequisites:
+ Git is installed
+ Java 17 Installed 
+ Maven is installed
+ AWS RDS MYSQL is created

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  
### Step 2: Create the Jenkins Freestyle job
```xml
Job Name: build-freestyle
```
### Step 3: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/microservice-one.git
Branch : bbuild-freestyle
```
### Step 4: Build the application
```sh
mvn clean package
```
### Step 5: Verify whether artifact(jar) is generated or not
#### Congratulations. You have successfully generated the jar file using Jenkins Freestyle job.

