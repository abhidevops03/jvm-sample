pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '2'))
    }
    stages {
           
        stage('maven build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('junit'){
            steps {
                junit stdioRetention: '', testResults: 'target/surefire-reports/*.xml'
            }
        }
        stage('upload to nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'MavenHelloWorld', classifier: '', file: 'target/MavenHelloWorld-1.0.0-SNAPSHOT.jar', type: '.jar']], credentialsId: 'jenkins-nexus-id', groupId: 'com.devops.demo', nexusUrl: '34.82.170.107:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'pipeline-maven-repo', version: '1.0.0-SNAPSHOT'
            }
        }
        
        stage('archive artifact'){
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
                
    }
    
}
