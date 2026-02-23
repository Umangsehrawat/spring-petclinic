pipeline {
    agent any

    triggers {
        // every 5 minutes on Mondays
        cron('H/5 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Build') {
            steps { bat 'gradlew.bat clean build' }
        }

        stage('Test Coverage (JaCoCo)') {
            steps { bat 'gradlew.bat test jacocoTestReport' }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
        }
    }
}
