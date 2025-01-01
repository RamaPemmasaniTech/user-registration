# user-registration-page
+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://techworldwithmurali.com </br>
+ <b>Youtube Channel:</b>Tech World With Murali</br>
+ <b>Description:</b> Below are the steps outlined for manually Dockerizing and Pushing to AWS ECR.</br>

## Manually - Dockerizing and Pushing to AWS ECR

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ AWS ECR repository is created
+ AWS EKS is created
+ IAM User is created
+ kubectl is installed
+ aws cli is installed
+ Deployed the AWS ALB Ingress Controller
+ Deployed ExternalDNS

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/user-registration.git
  Branch Name: deploy-to-eks-ecr
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the repository in AWS ECR
```xml
Repository Name: user-registration
```
### Step 4: Write the Dockerfile
```xml
# Use an OpenJDK base image
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the target directory
COPY target/*.jar /app/user-registration.jar

# Expose the application's port (update if your application uses a specific port)
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "/app/user-registration.jar"]
```
### Step 5: Build and tag the Docker image
```xml
docker build . --tag user-registration:latest

docker tag user-registration:latest 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
```
### Step 6: Login to AWS ECR in local
```xml
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 266735810449.dkr.ecr.us-east-1.amazonaws.com
```

### Step 7: Push the docker image to DockerHub
```xml
docker push 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
```
### Step 8: Verify whether docker image is pushed or not in AWS ECR

### Step 9 : Write the Kubernetes Deployment and Service manifest files.
##### deployment.yaml
```xml


apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-registration
  namespace: user-management
spec:
  replicas: 2
  selector:
    matchLabels:
      app: user-registration
  template:
    metadata:
      labels:
        app: user-registration
    spec:
      containers:
      - name: user-registration
        image: 266735810449.dkr.ecr.us-east-1.amazonaws.com/user-registration:latest
```
##### service.yaml
```xml


apiVersion: v1
kind: Service
metadata:
  name: user-registration
  namespace: user-management
spec:
  selector:
    app: user-registration
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 8080
  type: NodePort
```
### Step 10: Update the Dockerhub image in deployment.yaml
### Step 11: Configure  to the AWS CLI using Access key ID & Secret access key
```xml
aws configure --profile dev
```
### Step 12: Connect to the AWS EKS Cluster
```xml
aws eks update-kubeconfig --name dev-cluster --region us-east-1 --profile dev
````
### Step 13: Apply the Kubernetes manifest files
```
kubectl apply -f .
```
### Step 14: Verify wether pods are running or not
```
kubectl get pods -n user-management
```
### Step 15: Access java application through NodePort.
```xml
http://Node-IP:port
```
### Step 16: Deploy Ingress Resource for This Application
```xml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: user-management
  namespace: user-management
  annotations:
    alb.ingress.kubernetes.io/scheme: internal
    alb.ingress.kubernetes.io/tags: app=techworldwithmurali,Team=DevOps
    alb.ingress.kubernetes.io/certificate-arn: arn:aws:acm:us-east-1:266735810449:certificate/8a7cbcb1-774c-463f-ab3e-476437028686
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTP": 80}, {"HTTPS":443}]'
    alb.ingress.kubernetes.io/ssl-redirect: '443'
    alb.ingress.kubernetes.io/security-groups: sg-026c5ab74985fa179

spec:
  ingressClassName: alb
  rules:
    - host: user-registration-dev.techworldwithmurali.in
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: user-registration
                port:
                  number: 8080
```
### Step 17: Apply the ingress

kubectl apply -f user-management-ingress.yaml

### Step 18: Check Whether Load Balancer, Rules, and DNS Records Are Created in Route 53

### Step 19: Access java application through DNS record Name.
```
https://user-registration-dev.techworldwithmurali.in
```


#### Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS).
