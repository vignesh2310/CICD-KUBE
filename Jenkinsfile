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
                withSonarQubeEnv(credentialsId: 'sonartoken') {
                 sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}