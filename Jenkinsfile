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
        stage ('simple-build') {
            steps {
                dir("tag"){
                    bat 'docker image tag api-produto lucius28/api-produtoPush'
                    echo 'Tag Realizada com sucesso'
                }
                dir("push"){
                    bat 'docker image push lucius28/api-produtoPush'
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