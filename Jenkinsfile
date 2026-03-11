pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Código fuente descargado exitosamente'
            }
        }

        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
                echo 'Dependencias instaladas correctamente'
            }
        }

        stage('Test') {
            steps {
                sh 'python -m pytest tests/ -v --tb=short'
            }
        }

        stage('Deploy Simulation') {
            steps {
                echo '=== SIMULACIÓN DE DESPLIEGUE ==='
                echo "Construyendo imagen Docker..."
                sh 'docker build -t devops-demo-app:latest .'
                echo "Imagen construida: devops-demo-app:latest"
                echo '=== DESPLIEGUE SIMULADO EXITOSAMENTE ==='
            }
        }
    }

    post {
        success {
            echo 'Pipeline ejecutado exitosamente.'
        }
        failure {
            echo 'El pipeline ha fallado.'
        }
    }
}