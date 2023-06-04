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

        stage('quality gate analysis') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonartoken'
                }
            }
        }
    }
}