node {

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
