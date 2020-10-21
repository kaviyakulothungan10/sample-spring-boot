pipeline {
    agent none
        environment {
        ENV_DOCKER = credentials('dockerhub')
        DOCKERIMAGE = "ravindranathbarathy/sample-spring-boot"
    }
    stages {
        stage('build') {
            agent {
                docker { image 'gradle' }
            }
            steps {
                sh 'chmod +x gradlew && ./gradlew build'
            }
        }
        stage('sonarqube') {
        agent any
            steps {
                script {
                    app = docker.build("${DOCKERIMAGE}:${env.BUILD_NUMBER}")      
                }
            }
        }
        stage('docker build') {
        agent any
            steps {
                script {
                    app = docker.build("${DOCKERIMAGE}:${env.BUILD_NUMBER}")      
                }
            }
            }
        }
}