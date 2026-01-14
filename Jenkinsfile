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
                sh 'docker compose -p saleserp build'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker compose -p saleserp up -d'
            }
        }
    }
}


