pipeline {
    agent {
        any
    }
    stages {
        stage('build') {
            agent { docker { image 'gradle' } }
            steps {
                sh 'chmod +x gradlew && ./gradlew build'
            }
        }
    }
}