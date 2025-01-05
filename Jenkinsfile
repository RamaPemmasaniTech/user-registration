  pipeline {
    agent any
parameters {
        string(name: 'BRANCH', defaultValue: 'deploy-to-eks-dockerhub-jenkinsfile', description: 'Git branch to clone')
	string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker Image Tag to deploy')

    }
	   environment {
        AWS_REGION = 'us-east-1'
        EKS_CLUSTER = 'dev-cluster'
	DEPLOYMENT_FILE = 'k8s/deployment.yaml'
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


	    stage('Update Deployment File') {
            steps {
                script {
                    sh """
                    sed -i 's|__TAG__|${params.IMAGE_TAG}|g' ${DEPLOYMENT_FILE}
                    cat ${DEPLOYMENT_FILE}
                    """
                }
            }
        }


	    stage('Apply Kubernetes Manifests') {
            steps {
                script {
                    sh """
                    cd k8s
                    kubectl apply -f deployment.yaml
		     kubectl apply -f service.yaml
                     kubectl apply -f secret.yaml
                    """
                }
            }
        }




      
        }
		
  }
