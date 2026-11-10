pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Java application'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
    steps {
        echo 'Running test cases'
        sh 'mvn test'

        echo 'Introducing an intentional failure'
        sh 'exit 1'
    }
}

        stage('Package') {
            steps {
                echo 'Creating JAR file'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
