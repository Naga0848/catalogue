pipeline {
    agent {
        label 'AGENT-1'
    }
     environment { 
        appVersion = ''
     }
    stages {
        stage('Read package.json') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Package version: ${appVersion}"
                }
            }
        }
        stage('Installing Dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}