
/*
pipeline {

    agent any

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/arunessential/arunessential-cicd.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t netflix-devops:latest .'
            }
        }

    }
}
*/
/*
pipeline {

    agent any

    environment {
        AWS_REGION = "us-east-1"
        ECR_REPO = "<ECR_URL>/netflix-devops"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t netflix-devops .'
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin <ECR_URL>

                docker tag netflix-devops:latest $ECR_REPO:latest
                docker push $ECR_REPO:latest
                '''
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                kubectl apply -f deployment.yml
                kubectl apply -f service.yml
                '''
            }
        }

    }
}
*/

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

stage('SonarQube Analysis') {
steps {
withSonarQubeEnv('SonarServer') {
sh 'sonar-scanner'
}
}
}
  
stage('Upload Artifact to Nexus'){
steps{
sh 'mvn deploy'
}
}
stage('Docker Build') {
            steps {
                sh 'docker build -t netflix-devops:latest .'
            }
        }
 
/*       
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
*/
