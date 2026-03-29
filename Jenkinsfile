node {
    checkout scm

    // Build
    stage("Build") {
        docker.image('shippingdocker/php-composer:8.2').inside('-u root') {
            sh 'rm composer.lock'
            sh 'composer install'
        }
    }

    // Testing
    docker.image('ubuntu').inside('-u root') {
        sh 'echo "Ini adalah test"'
    }
}
node {
    checkout scm

    // Build
    stage("Build") {
        docker.image('composer:latest').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist --ignore-platform-reqs'
        }
    }

    // Testing
    docker.image('ubuntu').inside('-u root') {
        sh 'echo "Ini adalah test"'
    }
}
