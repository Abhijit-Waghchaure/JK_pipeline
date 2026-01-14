pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
        jdk 'JDK_21'
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
