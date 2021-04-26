pipeline {
    agent any
    tools {
    maven 'maven3'
  }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('clean workstation'){
                steps{
            cleanWs()
        }
        }
        stage('Git checkout') {
            steps {
                git branch: 'develop', credentialsId: 'ff8d9146-de5d-43ee-9ff7-adaa9c888197', url: 'https://github.com/DevOpsMallesh/java-hello-world-with-maven.git'
            }
        }
        stage('build') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        
        
    }
}
