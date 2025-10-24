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
        stage('Register in DB'){
            steps{
                script{
                    def commit = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                    def status = currentBuild.currentResult

                    echo "Registrando en la BD: ${commit} - ${status}"

                    //Conexión JDBC
                    @Grab('mysql:mysql-connector-java:8.0.33')
                    import groovy.sql.Sql
                    
                    def sql = Sql.newInstance(
                        'jdbc:mysql://host.docker.internal:3307/jenkins_db',
                        'root',
                        'root',
                        'com.mysql.cj.jdbc.Driver'
                    )

                    sql.execute("INSERT INTO build_status (commit_hash, status) VALUES (?,?)", [commit, status])
                    sql.close
                }
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
