pipeline {

agent any

stages {

stage('Git Checkout'){
steps{
git branch: 'main', url: 'https://github.com/arunessential/arunessential-cicd.git'
}
}

stage('Build'){
steps{
sh 'mvn clean package'
}
}

stage('Unit Test'){
steps{
sh 'mvn test'
}
}

stage('Upload Artifact to Nexus'){
steps{
sh 'mvn deploy'
}
}

stage('Docker Build'){
steps{
sh 'docker build -t netflix-devops .'
}
}

stage('Push Image to ECR'){
steps{
sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <ECR_URL>'
sh 'docker tag netflix-devops:latest <ECR_URL>/netflix-devops:latest'
sh 'docker push <ECR_URL>/netflix-devops:latest'
}
}

stage('Deploy to EKS'){
steps{
sh 'kubectl apply -f k8s/deployment.yaml'
sh 'kubectl apply -f k8s/service.yaml'
}
}

}

}
