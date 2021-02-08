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
            }
        }
        
        stage ('Stage package') {
            steps {
                bat './mvnw package -DskipTests'
            }
        }
        
        stage ('Stage archivage') {
            steps {
                script {
                    nexusArtifactUploader artifacts: [
                       [artifactId: 'spring-petclinic', classifier: 'debug', file: 'target/spring-petclinic-2.4.2.jar', type: 'jar']
                    ], 
                    credentialsId: '44620c50-1589-4617-a677-7563985e46e1', 
                    groupId: 'sp.sd', 
                    nexusUrl: 'localhost:8081/', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'NexusArtifactUploader', 
                    version: '3.29'
                }
            }
        }
        
        stage ('Stage Deploy') {
            steps {
                bat './deploy.sh'
            }
        }
        
    }
}
