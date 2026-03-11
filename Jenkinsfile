pipeline {

    agent any

    stages {

        stage('Build') {
            agent {
                docker {
                    image 'python:3.10'
                    reuseNode true
                }
            }
            steps {
                echo 'Instalando dependencias...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'python:3.10'
                    reuseNode true
                }
            }
            steps {
                echo 'Ejecutando pruebas...'
                sh 'pip install -r requirements.txt && pytest tests/ -v --tb=short'
            }
        }

        stage('Deploy Simulation') {
            steps {
                echo '=== SIMULACIÓN DE DESPLIEGUE ==='
                echo 'Construyendo imagen Docker...'
                sh 'docker build -t devops-demo-app:latest .'
                echo 'Imagen construida: devops-demo-app:latest'
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