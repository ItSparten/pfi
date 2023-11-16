pipeline {
    agent any

   
    stages {
        stage('Récupération du code') {
            steps {
                checkout scm
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t abderrahmenamri-5nids2-g10 .'
            }
        }
stage('trivy') {
            steps {
                    sh 'trivy sonarqube:latest'
                
            }
        }

        
        
        
    }
}




