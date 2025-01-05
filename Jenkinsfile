  pipeline {
    agent any
parameters {
        string(name: 'BRANCH', defaultValue: 'deploy-to-eks-dockerhub-jenkinsfile', description: 'Git branch to clone')

    }
	  
    stages {
stage('Clone') {
            steps {
                git branch: "${params.BRANCH}", credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }




      
        }
		
  }
