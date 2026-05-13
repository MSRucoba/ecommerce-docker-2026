pipeline {
    agent any

    tools {
        maven "MAVEN_HOME"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Clonando repositorio..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Compilando proyecto..."
                sh "mvn clean compile"
            }
        }

        stage('Package') {
            steps {
                echo "Empaquetando proyecto..."
                sh "mvn package -DskipTests"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo "Analizando con SonarQube..."
                withSonarQubeEnv('sonarqube') {
                    sh "mvn sonar:sonar -Dsonar.projectKey=ecommerce-docker-2026 -Dsonar.projectName=Ecommerce"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline OK"
        }
        failure {
            echo "Pipeline FAILED"
        }
    }
}