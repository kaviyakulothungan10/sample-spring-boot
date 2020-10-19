pipeline {
    agent none
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
                sh """export SONARQUBE_SCANNER_PARAMS={} && sonar-scanner -Dsonar.projectKey=sample-spring-boot -Dsonar.sources=. -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.java.binaries=build/classes/java/main"""
                }
            }
        }
    }
}