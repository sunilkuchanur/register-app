pipeline {
    agent { label 'maven-node' }
    tools {
        jdk 'Java-17'
        maven 'maven-3'
        git 'git'
    }
    environment {
            APP_NAME = "register-app-pipeline"
            RELEASE = "1.0.0"
            DOCKER_USER = "sunilkuchanur"
            DOCKER_PASS = 'DockerHub-Cred'
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages{
     stage("Cleanup Workspace"){
                steps {
                cleanWs()
      }
     }
     stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/sunilkuchanur/register-app.git'
      }
     }
     stage("Build Application"){
            steps {
                sh "mvn clean package"
      }
     }
     stage("Test Application"){
           steps {
                 sh "mvn test"
      }
     }
        
     stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }

       }
       
  }
}
