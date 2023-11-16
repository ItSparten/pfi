pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerid')
        DOCKER_IMAGE_TAG = '1.0.0'  // Define the Docker image tag here
    }

    stages {
        stage('Récupération du code') {
            steps {
                checkout scm
            }
        }

        

        stage('Maven Build and SonarQube Scan') {
            steps {
                sh 'mvn clean compile'
                sh 'mvn sonar:sonar -Dsonar.login=squ_e050fbc3eb84d4965c2a274608a0c587b00b7154'
            }
        }

        stage('Unit Tests with Mockito') {
            steps {
                sh 'mvn -Dtest=mockito test'
            }
        }


        stage('Maven Deploy') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t abderrahmenamri-5nids2-g10 .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh "docker tag abderrahmenamri-5nids2-g10 itsparten/abderrahmenamri-5nids2g10:${DOCKER_IMAGE_TAG}"
                sh "docker push itsparten/abderrahmenamri-5nids2g10:${DOCKER_IMAGE_TAG}"
            }
        }

        stage('Docker Compose Up') {
            steps {
                sh 'docker compose up -d'
            }
        }
         stage('Junit') {
                    steps {
                        sh 'mvn -Dtest=Junit test'
                    }
                }
         stage('Grafana/prometheus') {
            steps {
                sh 'docker start 8f7df022baac'
                sh 'docker start 26e6338b70a7'
            }
         }        
    }
}




