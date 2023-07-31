node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            checkout scm
            sh 'rm -rf node_modules'
            sh 'rm -f package-lock.json'
            sh 'rm -f yarn.lock'
            sh 'npm cache clean --force'
            sh 'npm install' 
        }
        stage('Test') { 
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sleep(time: 1, unit: 'MINUTES')
            sh './jenkins/scripts/kill.sh'
        }
    }
}