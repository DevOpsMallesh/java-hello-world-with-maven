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
        script{
        def mavenPom = readMavenPom file:'pom.xml'
          nexusArtifactUploader artifacts: [
          [
            artifactId: 'hello-world-maven', classifier: '', file: "target/hello-world-test-${mavenPom.version}.jar", type: 'jar'
          ]
        
          ], 
         credentialsId: 'jenkins-nexus', 
         groupId: 'devops1', 
         nexusUrl: '34.141.119.252:8081',
         nexusVersion: 'nexus3', 
         protocol: 'http', 
         repository: 'jenkins2-testing', 
         version: "${mavenPom.version}"
        }
      }
    }
  }
}
