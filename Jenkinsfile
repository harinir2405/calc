pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                echo 'Building Java Calculator'
                sh 'mvn clean package'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'

            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }

        failure {
            echo 'Build failed. Please check the console output.'
        }
    }
}
