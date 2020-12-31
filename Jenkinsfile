pipeline {
    agent any
    triggers { cron('*/5 * * * *') }
    options { timeout(time: 5) }
    stages {
        stage ("Docker build") {
            steps {
                echo 'docker-compose build'
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