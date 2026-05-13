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
                withCredentials([string(credentialsId: 'sonarqube-token-2026', variable: 'SONAR_TOKEN')]) {
                    sh """
                        mvn sonar:sonar \
                          -Dsonar.projectKey=ecommerce-docker-2026 \
                          -Dsonar.projectName=Ecommerce \
                          -Dsonar.host.url=http://sonarqube:9000 \
                          -Dsonar.token=${SONAR_TOKEN}
                    """
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