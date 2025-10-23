//groovy

pipeline {
    agent any

    stages{
        stage('Build'){
            steps {
                echo 'Compilando Java....'
                sh 'javac Main.java'
            }
        }

        stage('Test'){
            steps{
                echo 'Ejecutando etapa de Test con Groovy'
                sh 'java Main'
            }

        }

    }

    post {
        success {
            echo 'Pipeline ejecutado con éxito, enhorabuena!'
        }
        failure {
            echo 'Pipeline falló'
        }
    }
}
