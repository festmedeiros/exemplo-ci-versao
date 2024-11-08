pipeline {
    agent any

    environment {
        NODEJS_VERSION = 'nodejs-latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/festmedeiros/exemplo-ci-versao.git'
            }
        }

        stage('Install Dependencies') {
            tools {
                nodejs NODEJS_VERSION
            }
            steps {
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Versioning') {
            steps {
                script {
                    def version = bat(script: "git describe --tags --abbrev=0", returnStdout: true).trim()
                    echo "Version: ${version}"
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
