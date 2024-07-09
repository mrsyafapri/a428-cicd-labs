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

    stage('Deploy') {
        app.inside('-p 3000:3000') {
            sh './jenkins/scripts/deliver.sh' 
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
            sh './jenkins/scripts/kill.sh' 
        }
    }
}
