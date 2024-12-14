pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'deploy-to-eks-ecr-jenkinsfile', description: 'Git branch to clone')
       string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker Image Tag to deploy')
    }

    environment {
        AWS_REGION = 'us-east-1'
        EKS_CLUSTER = 'infra-cluster'
        DEPLOYMENT_FILE = 'k8s/deployment.yaml'
    }
   stages {

stage('Clone') {
            steps {
                git branch: "${params.BRANCH_NAME}", credentialsId: 'github-cred', url: 'https://github.com/techworldwithmurali/user-registration.git'
            }
        }

       stage('Set Up AWS EKS Config') {
            steps {
                script {
                    sh """
                    aws eks update-kubeconfig --name ${EKS_CLUSTER} --region ${AWS_REGION}
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


     
   }
}
