pipeline {
    agent { label 'slave-node'}

    environment {
        // Set your ECR registry URL
        ECR_REGISTRY = "287489840086.dkr.ecr.ap-southeast-1.amazonaws.com/super30_ecr"
        // Set the name of your Docker image
        dockerImageTag = "${env.BUILD_NUMBER}"


    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/venugopalsgnew/jenkins_ecr_repo.git']])
            }
        }

        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${ECR_REGISTRY}:${dockerImageTag}")
                }
            }
        }

        stage('Pushing to ECR') {
            steps {
                script {

                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 288214676350.dkr.ecr.ap-south-1.amazonaws.com'
                    sh "docker push ${ECR_REGISTRY}:${dockerImageTag}"
                }
            }
        }

    }
      
}
