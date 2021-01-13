pipeline {
    agent any
    triggers { cron('*/5 * * * *') }
    options { timeout(time: 5) }
    environment {
        DJANGO_DEBUG = credentials('booktime-django-debug')
        SECRET_KEY    = credentials('booktime-secret-key')
        DJANGO_ALLOWED_HOSTS = credentials('booktime-allowed-host')
        REGISTRY_HOST = credentials('booktime-docker-registry')
    }
    stages {
        stage ("Build") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml build'
            }
        }
        stage ("Push Image") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml push'
            }
        }
        stage ("Unit Test") {
            try {
                sh 'docker-compose -f docker-compose.tests.yml up'
            } catch (err) {
                mattermostSend (
                color: "danger",
                message: "Build FAILED AT STAGE <UNIT TEST>: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
                )
            }
        }
    }
    post {
        always {
            sh 'docker-compose -f docker-compose.tests.yml down'
        }
        success {
             mattermostSend (
                color: "good",
                message: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
                )
        }
        failure {
            mattermostSend (
                color: "danger",
                message: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
                )
        }
    }
}