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
        agent {
            docker { image 'sonarsource/sonar-scanner-cli' } }
            steps {
                withSonarQubeEnv("sonarcloud") {
                sh """export SONARQUBE_SCANNER_PARAMS={} && sonar-scanner -Dsonar.projectKey=sample-spring-boot -Dsonar.sources=. -Dsonar.organization=mydevopstestlab -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.java.binaries=build/classes/java/main"""
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
        stage('docker build') {
        agent any
            steps {
                script {
                    /* Finally, we'll push the image with two tags:
                    * First, the incremental build number from Jenkins
                    * Second, the 'latest' tag.
                    * Pushing multiple tags is cheap, as all the layers are reused. */
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }

            }
            }
        }
}
}