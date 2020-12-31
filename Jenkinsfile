pipeline {
    agent any
    triggers { cron('* * * * *') }
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
    }
    post {
        always {
            sleep 300
            echo 'docker-compose build'
        }
    }
}