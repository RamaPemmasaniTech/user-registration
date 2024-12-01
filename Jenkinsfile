pipeline {
    agent any
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'helm-deploy-on-eks-ecr-jenkinsfile', description: 'Git branch to clone')
    }
    stages {
stage('Clone') {
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

      
	}
	}
