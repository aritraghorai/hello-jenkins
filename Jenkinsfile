pipeline {
    agent any
    tools { nodejs "node" }
    environment {
        imageName= "aritraghorai/react-app"
        registryCredential= "aritraghorai"
        dockerImage=''
        DOCKER_CRED=credentials('docker-hub-cred')
    }
    stages {
        stage("Build Image") {
             steps{
                script {
                    dockerImage = docker.build imageName
                }
             }
        }
        stage("docker login") {
             steps {
                sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin '
             }
        }
        stage("docker login") {
             steps {
                script {
                     dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
             }
        }
        post{
            always{
                sh 'docker logout'
            }
        }
}
