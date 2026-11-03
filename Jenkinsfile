
pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'staging', 'production'],
            description: 'Select deployment environment'
        )

        string(
            name: 'APP_VERSION',
            defaultValue: '1.0.0',
            description: 'Application version'
        )
    }

    environment {
        APP_NAME = 'my-devops-app'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"

                sh '''
                    echo "Application: $APP_NAME"
                    echo "Version: $APP_VERSION"
                    echo "Environment: $ENVIRONMENT"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'

                sh '''
                    test -f readme
                    echo "Tests passed"
                '''
            }
        }

        stage('Parallel Checks') {
            parallel {

                stage('Code Check') {
                    steps {
                        echo 'Running code checks'
                        sh 'echo Code check completed'
                    }
                }

                stage('Security Check') {
                    steps {
                        echo 'Running security checks'
                        sh 'echo Security check completed'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENVIRONMENT}"
                echo "Version: ${params.APP_VERSION}"
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

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
