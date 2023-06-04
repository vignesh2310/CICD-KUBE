pipeline {
    agent any 
    tools {
        maven "maven3"
    }
    stages {
        stage('static sonar analysis') {
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