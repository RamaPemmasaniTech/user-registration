pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}


    stages {
       stage('Clone the repo') {
            steps {
                git branch: 'pushing-docker-image-to-dockerhub-jenkinsfile', credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
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
                IMAGE_TAG=$(echo $GIT_COMMIT | cut -c1-6)
               docker build . --tag user-registration:$IMAGE_TAG
               docker tag user-registration:$IMAGE_TAG mmreddy424/user-registration:$IMAGE_TAG
                
                '''
                
            }
        }
     
        stage('Push the docker image to dockerhub') {
            steps {
                sh '''
                  IMAGE_TAG=$(echo $GIT_COMMIT | cut -c1-6)
               docker login -u mmreddy424 -p Docker@2580
               docker  push mmreddy424/user-registration:$IMAGE_TAG
                
                '''
                
            }
        }   
        
        
        
    }
}
