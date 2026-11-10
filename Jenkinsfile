
pipeline {
    agent any
    parameters {
    choice(
        name: 'BUILD_ENV',
        choices: ['development', 'testing', 'production'],
        description: 'Select the environment for this build'
    )
}

    environment {
        APP_NAME = 'Java Calculator'
    }

    stages {
        stage('Development Deployment') {
    when {
        expression {
            params.BUILD_ENV == 'development'
        }
    }
    steps {
        echo 'Development environment selected'
        echo 'Deploying application to Development'
    }
}

stage('Testing Deployment') {
    when {
        expression {
            params.BUILD_ENV == 'testing'
        }
    }
    steps {
        echo 'Testing environment selected'
        echo 'Deploying application to Testing'
    }
}

stage('Production Deployment') {
    when {
        expression {
            params.BUILD_ENV == 'production'
        }
    }
    steps {
        echo 'Production environment selected'
        echo 'Deploying application to Production'
    }
}
        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                checkout scm
            }
        }
        stage('Build Information') {
            steps {
                echo "Application: ${env.APP_NAME}"
                echo "Selected Environment: ${params.BUILD_ENV}"
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
                echo "Build URL: ${env.BUILD_URL}"
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
