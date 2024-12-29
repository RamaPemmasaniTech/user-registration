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
               docker build . --tag user-registration:$GIT_COMMIT
               docker tag user-registration:$GIT_COMMIT mmreddy424/user-registration:$GIT_COMMIT
                
                '''
                
            }
        }
     
        stage('Push the docker image to dockerhub') {
            steps {
                sh '''
               docker login -u mmreddy424 -p Docker@2580
               docker  push mmreddy424/user-registration:$GIT_COMMIT
                
                '''
                
            }
        }   
        
        
        
    }
}
