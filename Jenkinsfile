pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

    parameters {
	     string(name: 'BRANCH', defaultValue: 'pushing-docker-image-to-ecr-jenkinsfile', description: 'Branch to build')
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
		IMAGE_TAG=$(echo $GIT_COMMIT | cut -c1-6)
              docker build . --tag user-registration:$IMAGE_TAG
              docker tag user-registration:$IMAGE_TAG 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:$IMAGE_TAG
                
                '''
                
            }
        }
        
        
        stage('Push Docker Image to AWS ECR') {
steps{
                    sh '''
		    IMAGE_TAG=$(echo $GIT_COMMIT | cut -c1-6)
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 266735810449.dkr.ecr.us-east-1.amazonaws.com
                   docker push 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:$IMAGE_TAG
                    '''
            } 

        }
        
     
        
        
     
        
    }
}
