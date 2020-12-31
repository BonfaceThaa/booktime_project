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
        stage ("Docker build") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml build'
            }
        }
        stage ("Docker Run Tests") {
            steps {
                sh 'docker-compose -f docker-compose.tests.yml up'
            }
        }
    }
    post {
        always {
            echo 'docker-compose down'
        }
    }
}