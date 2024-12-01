
pipeline {
    agent any

    stages {
      
stage('Clone THE REPOSITORY') {
            steps {
                git branch: 'helm-deploy-on-eks-dockerhub-jenkinsfile', credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }
    }
}
