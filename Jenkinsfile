pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deliver') {
            steps {
                sh 'npm run build'
                sh '''
                set -x
                npm start &
                sleep 1
                echo $! > .pidfile
                set +x
                '''
                echo 'Visit http://localhost:3000 to see your Node.js/React application in action.'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh '''
                set -x
                kill $(cat .pidfile)
                '''
            }
        }
    }
}
