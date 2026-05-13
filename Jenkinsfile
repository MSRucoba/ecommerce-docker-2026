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