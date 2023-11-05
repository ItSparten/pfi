pipeline {
    agent any

    

    stages {
        stage('Récupération du code') {
            steps {
                checkout scm
            }
        }

        stage('Lancement de la commande Maven') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('SonarQube Scan') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_e050fbc3eb84d4965c2a274608a0c587b00b7154'
            }
        }
        stage("mockito"){
                    steps {
                        sh 'mvn -Dtest=mockito test'
                    }
                }
     
       stage('mvn deploy'){
            steps {
                sh "mvn deploy"
            }
       }

      


       stage('Docker Compose') {
                   steps {
                       sh 'docker compose up -d'
                   }
       }


}

}



