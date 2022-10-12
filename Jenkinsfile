pipeline {
    agent any
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("divyadronavalli/demo:${TAG}")
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {
                        docker.image("divyadronavalli/demo:${TAG}").push()
                        docker.image("divyadronavalli/demo:${TAG}").push("latest")
                    }
                }
            }
        }
        stage('Deploy'){
            steps {
                sh "docker stop demo | true"
                sh "docker rm demo | true"
                sh "docker run --name demo -d -p 9004:8090 divyadronavalli/demo:${TAG}"
            }
        }
    }
}