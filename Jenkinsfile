pipeline {
    agent any
    tools {
    maven 'Maven3'
  }
	environment {
        NEXUS_COMMON_CREDS = credentials('nexus3')
        NEXUS_URL = 'http://44.192.22.223:8081/'
			    }
    stages {
	    stage('initialize maven'){
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
                }
			}
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
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, followSymlinks: false, onlyIfSuccessful: true
            }
        }    
	    stage('upload to nexus'){
		    steps{
			    
	nexusArtifactUploader artifacts: [[artifactId: 'hello-world', classifier: '', file: 'hello-world-1.0.0.jar', type: 'jar']], credentialsId: '{NEXUS_COMMON_CREDS}', groupId: 'devops', nexusUrl: '{NEXUS_URL}', nexusVersion: 'nexus3', protocol: 'http', repository: 'Devops', version: '1.0.0'
    
		    }	
	    }
        
    }
}
