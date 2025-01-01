pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

    parameters {
	     string(name: 'BRANCH', defaultValue: 'pushing-docker-image-to-ecr-jenkinsfile', description: 'Branch to build')
    }
 environment {
        // Define IMAGE_TAG globally using the GIT_COMMIT environment variable
        IMAGE_TAG = "${GIT_COMMIT.substring(0, 6)}"
    }

    stages {
       stage('Clone the repository') {
            steps {
               git branch: "${params.BRANCH}", credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }
        
        stage('Build the application') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        
      stage('Build Docker Image') {
            steps {
                sh '''
              docker build . --tag user-registration:$IMAGE_TAG
              docker tag user-registration:$IMAGE_TAG 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:$IMAGE_TAG
                
                '''
                
            }
        }
        
        
        stage('Push Docker Image to AWS ECR') {
steps{
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 266735810449.dkr.ecr.us-east-1.amazonaws.com
                   docker push 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:$IMAGE_TAG
                    '''
            } 

        }
        
     
        
        
     
        
    }
}
