pipeline {
    agent {
        any
    }
    stages {
        stage('build') {
            agent {"gradle"}
            steps {
                sh 'chmod +x gradlew && ./gradlew build'
            }
        }
    }
}