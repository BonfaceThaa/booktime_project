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
    stage ("Unit Test") {
        try {
            sh 'docker-compose -f docker-compose.tests.yml up --exit-code-from web'
            } catch (err) {
                notifyFailure()
                throw err
            }
    }
    stage ("Push Image") {
        sh 'docker-compose -f docker-compose.tests.yml push'
    }
    notifySuccessful()
}

def notifySuccessful() {
    mattermostSend (
        color: "good",
        message: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
        )
}

def notifyFailure() {
    mattermostSend (
        color: "danger",
        message: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Link to build>)"
        )
}
