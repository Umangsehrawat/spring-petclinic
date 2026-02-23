pipeline {
    agent any

    triggers {
        // Every 5 minutes on Mondays
        cron('H/5 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                bat 'mvnw.cmd -B clean test package'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('JaCoCo Coverage') {
            steps {
                bat 'mvnw.cmd -B jacoco:report'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar,target/*.war', fingerprint: true
            }
        }
    }
}
