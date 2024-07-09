node {
    def app

    stage('Prepare Environment') {
        app = docker.image('node:16-buster-slim')
    }

    stage('Build') {
        app.inside('-p 3000:3000') {
            sh 'npm install'
        }
    }

    stage('Test') {
        app.inside('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        app.inside('-p 3000:3000') {
            sh './jenkins/scripts/deliver.sh'
        }
        // Jeda eksekusi selama 1 menit
        echo 'Menjeda eksekusi pipeline selama 1 menit untuk percobaan aplikasi...'
        sleep time: 1, unit: 'MINUTES'
    }
}
