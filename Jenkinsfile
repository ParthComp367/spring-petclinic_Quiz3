pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven' // Ensure Maven is installed in Jenkins
    }

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ParthComp367/spring-petclinic_Quiz3.git'
            }
        }

        stage('Build') {
            steps {
                bat '${MAVEN_HOME}/bin/mvn clean package'
            }
        }

        stage('Run Tests with Jacoco') {
            steps {
                bat '${MAVEN_HOME}/bin/mvn test jacoco:report'
            }
            post {
                success {
                    jacoco execPattern: '**/target/jacoco.exec'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
