pipeline {
    agent {
        label 'linux'
    }

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['DEV', 'QA', 'PROD'],

        booleanParam(
            name: 'RUN_TESTS',
            defaultValue: true,
        )
    }

    environment {
        APP_NAME = 'DemoApp'
        VERSION = '1.0'
    }

    stages {

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                echo "Version: ${VERSION}"
                echo "Environment: ${params.ENVIRONMENT}"
            }
        }

        stage('Test') {
            when {
                expression {
                    params.RUN_TESTS == true
                }
            }

            steps {
                echo 'Running tests...'
                echo 'Tests completed successfully'
            }
        }

        stage('Deploy') {
            when {
                expression {
                    params.ENVIRONMENT != 'DEV'
                }
            }

            steps {
                echo "Deploying ${APP_NAME} to ${params.ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}