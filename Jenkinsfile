pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Backend Validation') {
            steps {
                dir('backend') {
                    sh 'npm ci'
                    sh 'npm run check'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                dir('frontend') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }

        stage('Verify Build Artifacts') {
            steps {
                sh '''
                    test -f frontend/dist/index.html
                    echo "Frontend production build verified."
                '''
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check the stage logs.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
