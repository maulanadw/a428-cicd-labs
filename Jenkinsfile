node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            timeout(time: 1, unit: 'MINUTES') {
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)', ok: 'Proceed'
            }
            sleep 1m // wait for 1 minute
            sh './jenkins/scripts/kill.sh'
        }
    }
}