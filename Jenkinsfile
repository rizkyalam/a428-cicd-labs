node {
    checkout scm

    docker.image('node:lts-bullseye-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            input message: 'Lanjut tahap deploy? (Klik "Proceed" untuk ke teahap deploy)'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deploy-heroku.sh'

            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'

            sleep time: 60, unit: 'SECONDS'

            sh './jenkins/scripts/kill.sh'
        }
    }
}
