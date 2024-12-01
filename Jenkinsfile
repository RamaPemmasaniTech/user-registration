pipeline {
    agent any
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'helm-deploy-on-eks-ecr-jenkinsfile', description: 'Git branch to clone')
	        string(name: 'RELEASE_NAME', defaultValue: '', description: 'RELEASE_NAME')
		string(name: 'namespace', defaultValue: '', description: 'namespace to deploy')
		string(name: 'ImageTag', defaultValue: '', description: 'Docker Image Tag to deploy')
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

	    stage('Deploy the Application') {
            steps {
                script {
                    // Deploy the application with the provided parameters
                    sh '''
                    helm upgrade --install $RELEASE_NAME . --namespace $namespace  --set image.tag=$ImageTag --force --wait --timeout 600s
                    '''
                }
            }
        }

      
	}
	}
