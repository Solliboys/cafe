node {
    checkout scm

    // Build
    stage("Build") {
        docker.image('composer:latest').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist --ignore-platform-reqs'
        }
    }

    // Testing
    stage("Test") {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

    // Deploy
    stage("Deploy") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
            sshagent(credentials: ['ssh-prod']) {
                sh 'mkdir -p ~/.ssh'
                sh "ssh-keyscan -H $PROD_HOST > ~/.ssh/known_hosts"
                sh "rsync -rav --delete ./ solli@$PROD_HOST:/home/solli/cafe/cafe/ --exclude=.env --exclude=storage --exclude=.git"
            }
        }
    }
}
