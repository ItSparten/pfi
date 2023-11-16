pipeline {
    agent any

   
    stages {
        stage('Récupération du code') {
            steps {
                checkout scm
            }
        }
stage('trivy') {
            steps {
                    sh 'trivy sonarqube:latest'
                
            }
        }

        
        
        
    }
}




