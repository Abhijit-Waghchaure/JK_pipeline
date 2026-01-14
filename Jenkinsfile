pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
        jdk 'JDK_21'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                dir('sales') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker compose up -d'
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

