
pipeline {
    agent any
  parameters {
        string(name: 'BRANCH_NAME', defaultValue: '', description: 'Git branch to clone')
  }
    stages {
      
stage('Clone THE REPOSITORY') {
            steps {
                git branch: "${params.BRANCH_NAME}", credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }

         stage('Connect to the EKS Cluster') {
            steps {
                script {
                    // Ensure AWS CLI is configured with the right credentials before this step
                    sh '''
                    aws eks update-kubeconfig --name dev-cluster --region us-east-1
                    kubectl get nodes
                    '''
                }
            }
        }

        stage('Deploy the Application') {
            steps {
                script {
                    // Deploy the application with the provided parameters
                    sh '''
                    cd helm-chart
                    helm upgrade --install -f values-dev.yaml user-registration . -n user-management
                    
                    '''
                }
            }
        }
    }
}
