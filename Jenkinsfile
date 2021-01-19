node {
    environment {
        DJANGO_DEBUG = credentials('booktime-django-debug')
        SECRET_KEY    = credentials('booktime-secret-key')
        DJANGO_ALLOWED_HOSTS = credentials('booktime-allowed-host')
        REGISTRY_HOST = credentials('booktime-docker-registry')
    }
    stage ("Build") {
        sh 'docker-compose -f docker-compose.tests.yml build'
        }
    stage ("Push Image") {
        sh 'docker-compose -f docker-compose.tests.yml push'
    }
    stage ("Unit Test") {
        try {
            sh 'docker-compose -f docker-compose.tests.yml up'
            } catch (err) {
                mattermostSend (
                color: "danger",
                message: "Build FAILED AT STAGE <UNIT TEST>: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
                )
                throw err
            }
    }
    notifySuccessful()
}

def notifySuccessful() {
    mattermostSend (
        color: "danger",
        message: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
        )
}