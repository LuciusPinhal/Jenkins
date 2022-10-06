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

        stage ('Push Image') {
            steps {
                script {
                    //criar credencial(autênticar) no Jenkis
                    docker.withRegistry('https://login.docker.com/u/login/identifier?state=hKFo2SBRM3VoYktrbFVUZ2ZBTXMwYXUxR3doMXdzQkV0RUlJT6Fur3VuaXZlcnNhbC1sb2dpbqN0aWTZIGZLajI4c3pnZXRRU3VZQ0FQcUZiZ0M4N3dTRGxiNFJDo2NpZNkgbHZlOUdHbDhKdFNVcm5lUTFFVnVDMGxiakhkaTluYjk', 'dockerhub') {
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