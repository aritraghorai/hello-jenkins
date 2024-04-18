pipeline {
    agent any
    tools { nodejs "node" }
    environment {
        imageName= "aritraghorai/react-app"
        registryCredential= "aritraghorai"
        dockerImage=''
    }
    stages {
        stage("Build Image") {
             steps{
                script {
                    dockerImage = docker.build imageName
                }
             }
        }
        stage("deploy image") {
             steps {
                script {
                    docker.withRegistry("https://hub.docker.com","docker-hub-cred"){
                     dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
             }
        }
    }
}
