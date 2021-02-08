pipeline {
    agent any
    stages {

        stage ('SCM checkout') {
            steps {
                git credentialsId: 'kenza-gif', url: 'https://github.com/kenza-gif/spring-petclinic.git'
            }
        }

        stage ('Stage build') {
            steps {
                bat './mvnw clean'
                bat './mvnw spring-javaformat:apply'
                bat './mvnw install -DskipTests'
            }
        }

        stage ('Stage Test') {
            steps {
                bat './mvnw test'
            }
        }
        
        stage ('Stage Analyse de code') {
            steps {
                bat "./mvnw checkstyle:checkstyle"
                recordIssues(tools: [checkStyle(reportEncoding: 'UTF-8')])
            }
        }
        
        stage ('Stage package') {
            steps {
                bat './mvnw package -DskipTests'
            }
        }
        
        stage ('Stage archivage') {
            steps {
                bat './mvnw deploy -DskipTests'
            }
        }
        
        stage ('Stage Deploy') {
            steps {
                bat './deploy.sh'
            }
        }
        
    }
}
