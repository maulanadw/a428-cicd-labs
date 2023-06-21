node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed', submitter: 'maulanadw'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            timeout(time: 1, unit: 'MINUTES') {
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)', ok: 'Proceed'
            }
            sleep 60 // wait for 1 minute
            sh './jenkins/scripts/kill.sh'
        }
    }
}