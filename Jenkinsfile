pipeline {
    agent any

    triggers {
        cron('H/5 * * * 1')
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'gradlew clean build'
            }
        }

        stage('Test Coverage') {
            steps {
                bat 'gradlew jacocoTestReport'
            }
        }
    }

    post {
        always {
            jacoco execPattern: '**/build/jacoco/test.exec',
                   classPattern: '**/classes',
                   sourcePattern: '**/src/main/java'
        }
    }
}
