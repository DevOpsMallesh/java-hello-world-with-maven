pipeline {
  agent any
  tools {
    maven 'Maven3'
  }
  stages{
    stage('Build'){
      steps{
        sh script: 'mvn clean package'
      }
    }
    stage('upload to nexus'){
      steps{
        def mavenPom = readMavenPom 'pom.xml'
          nexusArtifactUploader artifacts: [
          [
            artifactId: 'hello-world-maven', classifier: '', file: "target/hello-world-maven-${mavenPom.version}.jar", type: 'jar'
          ]
        
          ], 
         credentialsId: 'nexus3', 
         groupId: 'org.springframework', 
         nexusUrl: '3.238.96.180:8081',
         nexusVersion: 'nexus3', 
         protocol: 'http', 
         repository: 'Devops', 
         version: "${mavenPom.version}"
      }
    }
  }
}
