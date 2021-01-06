pipeline {
    agent any
    triggers { cron('*/5 * * * *') }
    options { timeout(time: 5) }
    environment {
        DJANGO_DEBUG = credentials('booktime-django-debug')
        SECRET_KEY    = credentials('booktime-secret-key')
        DJANGO_ALLOWED_HOSTS = credentials('booktime-allowed-host')
    }
    stages {
        stage ("Build") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml build'
            }
        }
        stage ("Unit Test") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml up'
            }
        }
    }
    post {
        always {
            sh 'docker-compose -f docker-compose.tests.yml down'
        }
        failure {
            mattermostSend (
                color: "danger",
                message: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
                )
        }
    }
}