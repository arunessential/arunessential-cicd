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
    }
}
