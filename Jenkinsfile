pipeline {
    agent any
    environment {
        DATABASE_URI = credentials("DATABASE_URI")
        SECRET_KEY = credentials("SECRET_KEY")
//         DOCKER_LOGIN = credentials("DOCKER_LOGIN")
        rebuild_db = 'true'
    }
    stages {
        stage('Test') {
            steps {
                sh 'bash jenkins/test.sh'
            }
        }
        stage('Setup Docker') {
            steps {
                sh 'bash jenkins/setup-docker.sh'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t navin-mawa/palette-generator1:latest .'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push navin-mawa/palette-generator1:latest'
            }
        }
        stage('Run') {
            steps {
                sh 'docker rm -f palette-generator1'
                sh 'docker run -d -p 80:5000 -e DATABASE_URI=$DATABASE_URI -e SECRET_KEY=$SECRET_KEY --name tpalette-generator1 navin-mawa/palette-generator1:latest'
                script{
                    if (env.rebuild_db == 'true') {
                        sh 'docker exec palette-generator1 python create.py'
                    }
                }
            }
        }
    }
    post {
        always {
            junit '**/*.xml'
            cobertura coberturaReportFile: 'coverage.xml', failNoReports: false
        }
    }
}
