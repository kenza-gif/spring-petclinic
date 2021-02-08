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
                    nexusArtifactUploader (
                        nexusVersion: 'nexus3'
                        protocol: 'http'
                        nexusUrl: 'localhost:8081/'
                        groupId: 'org.springframework.samples'
                        version: '2.4.2'
                        repository: 'NexusArtifactUploader'
                        credentialsId: 'd1c2e8a8-318b-4ff5-aa2c-c71b17ba1969'
                        artifact [
                            [ artifactId: 'spring-petclinic'
                            type: 'jar'
                            classifier: 'debug'
                            file: '**/target/spring-petclinic-2.4.2.jar' ]
                        ]
                    )
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
