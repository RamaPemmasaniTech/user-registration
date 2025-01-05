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


	    stage('Set Up AWS EKS Config') {
            steps {
                script {
                    sh """
                    aws eks update-kubeconfig --name ${EKS_CLUSTER} --region ${AWS_REGION}
                    aws sts get-caller-identity
		    kubectl get nodes
                    """
                }
            }
        }

	    




      
        }
		
  }
