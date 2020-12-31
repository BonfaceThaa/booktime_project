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
                sh 'docker-compose build'
            }
        }
        stage ("Docker Run") {
            steps {
                sh 'docker-compose up'
            }
        }
        stage ("Testing app") {
            steps {
                sh 'docker-compose exec web python booktime/manage.py test main'
            }
        }
    }
    post {
        always {
            echo 'docker-compose down'
        }
    }
}