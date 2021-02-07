// Instead of annotating an unnecessary import statement, the symbol _ is annotated, according to the annotation pattern.
@Library('adop-pluggable-scm-jenkinsfile') _

def repoName = "spring-petclinic"
def regRepo = "adop-cartridge-java-regression-tests"

pipeline {

        agent any
        environment{
            echo " project Info "
            ENVIRONMENT_NAME = 'CI'
        }

        stage ('SCM checkout') {
            git credentialsId: 'kenza-gif', url: 'https://github.com/kenza-gif/spring-petclinic.git'
        }

        stage ('Stage build') {
            sh "mvn clean build -DskipTests"
        }

        stage ('Stage Test') {
            sh "mvn test"
        }

}
