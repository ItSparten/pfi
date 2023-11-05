pipeline {
    agent any

    environment {
    		DOCKERHUB_CREDENTIALS=credentials('dockerid')
    	}
    

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

      
stage('Docker Image') {
                   steps {
                       sh 'sudo docker build -t abderrahmenamri-5nids2-g10 .'
                   }
       }

        stage('DOCKERHUB') {
                          steps {
                              sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                              sh 'docker tag abderrahmenamri-5nids2-g10 itsparten/abderrahmenamri-5nids2g10:1.0.0'
                              sh 'docker push itsparten/abderrahmenamri-5nids2g10:1.0.0'
                          }
                      }


       stage('Docker Compose') {
                   steps {
                       sh 'docker compose up -d'
                   }
       }


}

}



