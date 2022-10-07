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

    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
        stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

        stage ('Push Image') {
            steps {

				sh 'docker push api-produto:${env.BUILD_ID}'
		
                // script {
                //     //criar credencial(autênticar) no Jenkis
                //     docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                //         dockerapp.push('latest')
                //         dockerapp.push("${env.BUILD_ID}")
                //     }
                // }
            }
        }

        post {
		always {
			sh 'docker logout'
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