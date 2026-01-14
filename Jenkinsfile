pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    environment {
        DOCKER_IMAGE = "saleserp-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                dir('saleserp/sales') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Docker Build') {
            steps {
                dir('saleserp') {
                    sh 'docker compose build'
                }
            }
        }

        stage('Docker Deploy') {
            steps {
                dir('saleserp') {
                    sh 'docker compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo "SalesERP deployed successfully 🚀"
        }
        failure {
            echo "Build failed ❌"
        }
    }
}
