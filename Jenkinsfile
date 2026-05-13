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
                bat "mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                echo "Ejecutando tests..."
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "Empaquetando aplicación..."
                bat "mvn package -DskipTests"
            }
        }
    }

    post {
        success {
            echo '¡Pipeline ejecutado con éxito!'
        }
        failure {
            echo 'Pipeline falló.'
        }
    }
}