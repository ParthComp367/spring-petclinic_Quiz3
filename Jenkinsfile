pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Make sure the correct branch is being checked out
                git branch: 'main', url: 'https://github.com/pateldev11/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                // Build steps here
                bat 'mvn clean install'
            }
        }

        stage('Jacoco Coverage') {
            steps {
                // Jacoco coverage steps here
                bat 'mvn jacoco:prepare-agent test jacoco:report'
            }
        }

        stage('Package Artifact') {
            steps {
                // Package steps here
                bat 'mvn package'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Monday
    }
}