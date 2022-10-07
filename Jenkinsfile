pipeline {
    agent any
    stages {
        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("api-produto:${env.BUILD_ID}", '-f ./src/Dockerfile ./src') 
                }                
            }
        }
        stage ('Test Image') {
            steps {
                dir("Teste"){
                    bat 'docker image ls'
                    echo 'Teste realizado com sucesso'
                }
            }
        }
        stage ('simple-tag') {
            steps {
                dir("tag"){
                    bat 'docker image tag api-produto:45 lucius28/api-produto'
                    echo 'Tag Realizada com sucesso'
                }
            }
        }

        stage ('simple-push') {
            steps {
                dir("push"){
                    bat 'docker image push lucius28/api-produto'
                    echo 'Tag Realizada com sucesso'
                }
            }
        }
        stage ('Push Image no docker Hub') {
            steps {
                script {
                    //criar credencial ou token de acesso
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}