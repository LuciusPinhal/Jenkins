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

        stage ('Test Run') {
            steps {
                dir("run"){
                    bat 'docker container run -p 80:80 api-produtos:53'
                    echo 'Teste realizado com sucesso'
                     bat 'docker stop api-produtos:53'
                }
            }
        }
         stage ('Test container down') {
            steps {
                dir("down"){
                    bat 'docker stop api-produtos:53'
                    echo 'Teste realizado com sucesso'
                }
            }
        }
        // stage ('simple-tag') {
        //     steps {
        //         dir("tag"){
        //             bat 'docker image tag api-produto:49 lucius28/api-produto'
        //             echo 'Tag Realizada com sucesso'

        //             bat 'docker image push lucius28/api-produto'
        //             echo 'Push Realizada com sucesso'
                
        //         }
        //     }
        // }


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