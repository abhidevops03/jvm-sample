pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '2'))
    }
           
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
        
        stage('archive artifact'){
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
                
    }
    
    
}
