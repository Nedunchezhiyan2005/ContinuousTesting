pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Automated Tests') {
            steps {
                bat 'pytest --html=test-report.html --self-contained-html'
            }
        }

        stage('Analyze Test Results') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'test-report.html',
                    reportName: 'Automated Test Report'
                ])
            }
        }
    }

    post {
        always {
            echo 'Continuous Testing completed.'
        }

        success {
            echo 'All automated tests passed.'
        }

        failure {
            echo 'Automated tests failed.'
        }
    }
}