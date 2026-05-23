pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application'
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh 'kubectl apply -f k8s/staging/'
            }
        }

        stage('Smoke Test') {
            steps {
                sh '''
                kubectl rollout status deployment/kk-payments -n kijani-staging
                '''
            }
        }

        stage('Approval Gate') {
            steps {
                input(
                    message: 'Deploy to production?',
                    ok: 'Approve'
                )
            }
        }

        stage('Deploy to Production') {
            steps {
                sh 'kubectl apply -f k8s/production/'
            }
        }
    }
}
