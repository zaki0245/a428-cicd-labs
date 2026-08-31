node {
    // Ambil environment variable dari Jenkins yang sudah disetel
    withEnv([
        "DOCKER_HOST=tcp://docker:2376",
        "DOCKER_CERT_PATH=/certs/client",
        "DOCKER_TLS_VERIFY=1"
    ]) {
        stage('Checkout') {
            checkout scm
        }
        stage('Build') {
            docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                sh 'npm install'
            }
        }
        stage('Test') {
            docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}