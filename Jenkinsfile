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

        stage('Test') {
            steps {
                echo "Ejecutando tests..."
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "Empaquetando aplicacion..."
                sh "mvn package -DskipTests"
            }
        }
    }

    post {
        success {
            echo "Pipeline ejecutado con exito!"
        }
        failure {
            echo "Pipeline fallo."
        }
    }
}