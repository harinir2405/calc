
pipeline {
    agent any

    environment {
        APP_NAME = 'Java Calculator'
    }

    stages {

        stage('Build Information') {
            steps {
                echo "Application: ${env.APP_NAME}"
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
                echo "Build URL: ${env.BUILD_URL}"
            }
        }

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
