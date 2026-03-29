node {
    checkout scm

    stage("Build") {
        docker.image('composer:latest').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist --ignore-platform-reqs'
        }
    }

    docker.image('ubuntu').inside('-u root') {
        sh 'echo "Ini adalah test"'
    }
}
