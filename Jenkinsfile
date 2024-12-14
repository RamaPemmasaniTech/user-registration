pipeline {
    agent any
   stages {

stage('Clone') {
            steps {
                git branch: 'deploy-to-eks-ecr-jenkinsfile', credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }


     
   }
}
