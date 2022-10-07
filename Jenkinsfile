pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                sh 'docker build -t darinpope/dp-alpine:latest .'

                script {
                    dockerapp = docker.build("api-produto:${env.BUILD_ID}", '-f ./src/Dockerfile ./src') 
                }                
            }
        }

        stage ('Login DockerHub'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u DOCKERHUB_CREDENTIALS_USR --passoword-stdin'
            }

        }
        stage ('Push Image') {
            steps {
                script {
                    sh 'docker push darinpope/dp-alpine:latest'
                    // //criar credencial(autênticar) no Jenkis
                    // docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    //     dockerapp.push('latest')
                    //     dockerapp.push("${env.BUILD_ID}")
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