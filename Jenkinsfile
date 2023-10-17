pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and Publish') {
            when {
                expression { currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause) }
            }
            steps {
                sh "docker run -v /var/www/html:/var/www/html ubuntu:latest bash -c 'apt-get update && apt-get install -y apache2 && cp -r * /var/www/html/'"
            }
        }
        
        stage('Build') {
            when {
                expression { !currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause) }
            }
            steps {
                sh "docker run -v /var/www/html:/var/www/html ubuntu:latest bash -c 'apt-get update && apt-get install -y apache2'"
            }
        }
    }
}
