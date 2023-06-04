pipeline {
    agent any 
    tools {
        maven "maven3"
    }
    environment {
        VERSION = "${env.BUILD_ID}"
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

        stage('docker build & push to nexus') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'nexuspass', variable: 'nexuspass')]) {
                         sh '''
                           docker build -t 3.128.171.117:8083/springapp:${VERSION} .
                         '''
                    }
                   
                }
            }
        }
    }
}