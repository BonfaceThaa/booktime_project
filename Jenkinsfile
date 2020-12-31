pipeline {
    agent any
    triggers { cron('*/5 * * * *') }
    options { timeout(time: 5) }
    environment {
        DJANGO_DEBUG = '${env.DJANGO_DEBUG}'
        SECRET_KEY    = '${env.SECRET_KEY}'
        DJANGO_ALLOWED_HOSTS = '${env.DJANGO_ALLOWED_HOSTS}'
    }
    stages {
        stage ("Docker build") {
            steps {
                echo 'DJANGO_DEBUG = ${env.DJANGO_DEBUG}'
                echo 'SECRET_KEY = ${env.SECRET_KEY}'
                echo 'DJANGO_ALLOWED_HOSTS = ${env.DJANGO_ALLOWED_HOSTS}'
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