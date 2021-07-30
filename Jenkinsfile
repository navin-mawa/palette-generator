pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh "bash scripts/install.sh"
            }
        }
        stage('Testing') {
            steps {
                sh "bash scripts/test.sh"
            }
        }
        stage('Deploy') {
            steps {
                sh "bash scripts/deploy.sh"
            }
        }
    }
    post {
        always {
            cobertura coberturaReportFile: 'coverage.xml',  failNoReports: false
            junit 'junit.xml'
        }
    }
}