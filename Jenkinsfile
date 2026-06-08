pipeline {
    agent { label 'maven-node' }
    tools {
        jdk 'Java-17'
        maven 'maven-3'
        git 'git'
    }
    stages{
     stage("Cleanup Workspace"){
                steps {
                cleanWs()
      }
     }
     stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/sunilkuchanur/register-app.git'
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
        
  }
}
