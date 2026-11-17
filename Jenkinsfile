pipeline {

    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Java Maven project'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging Java application'
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying generated JAR file'

                bat '''
                if not exist deploy mkdir deploy
                copy /Y target\\jenkins-pipeline-project-1.0.jar deploy\\
                '''

                echo 'Deployment completed successfully'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Completed Successfully!'
        }

        failure {
            echo 'CI/CD Pipeline Failed!'
        }
    }
}