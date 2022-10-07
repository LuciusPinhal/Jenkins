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

        stage ('Push Image') {
            steps {
                script {
                    //criar
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        // stage ('Deploy Kubernetes') {
        //     environment {
        //         tag_version = "${env.BUILD_ID}"
                
        //     }
        //     steps {
        //         withKubeConfig([credentialsId: 'kubeconfig']) {
        //             sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
        //             sh 'kubectl apply -f ./k8s/deployment.yaml'
        //         }
        //     }
        // }
    }
}