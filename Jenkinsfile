pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9' // Name from Global Tool Configuration
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/HanvikaGuda/devops-Myautomation.git']])
                bat 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    bat "docker build -t krishnaguda23/devops-integration ."
                }
            }
        }

        stage('Push image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'mydockerpwd', variable: 'mypwd')]) {
                   // some block
                           bat "docker login -u krishnaguda23 -p ${mypwd}"
                    }
                    // Push the image to Docker Hub
                    bat "docker push krishnaguda23/devops-integration"
                }
            }
    }  }
}
