pipeline {
    agent any 
    stages {
        stage('static sonar analysis') {
            agent {
                docker {
                    image 'maven'
                }
            }
            steps {
                script {
                  withSonarQubeEnv(credentialsId: 'sonartoken') {
                  sh 'mvn clean package sonar:sonar'
                  }
                }
             
            }
        }
    }
}