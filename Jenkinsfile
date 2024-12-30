pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

    parameters {
	     string(name: 'BRANCH', defaultValue: '', description: 'Branch to build')
    }

    
 environment {
        // Define IMAGE_TAG globally using the GIT_COMMIT environment variable
        IMAGE_TAG = "${GIT_COMMIT.substring(0, 6)}"
    }
    stages {
       stage('Clone the repo') {
            steps {
                git branch: "${params.BRANCH}", credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
   
   stage('Build Docker Image') {
            steps {
                sh '''
               docker build . --tag user-registration:$IMAGE_TAG
               docker tag user-registration:$IMAGE_TAG mmreddy424/user-registration:$IMAGE_TAG
                
                '''
                
            }
        }
     
        stage('Push the docker image to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {

                sh '''
               docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD
               docker  push mmreddy424/user-registration:$IMAGE_TAG
                
                '''
                
            }
                }
        }   
        
        
        
    }
}
