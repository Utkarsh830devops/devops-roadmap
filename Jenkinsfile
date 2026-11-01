pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build started'

                sh '''
                    echo "Application Build"
                    echo "Build Number: $BUILD_NUMBER"
                    echo "Workspace: $WORKSPACE"

                    ls -la
                    echo "Build Successful"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests'

                sh '''
                    test -f readme
                    echo "README file exists"
                    echo "All tests passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage executed'
                echo 'Application ready for deployment'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
