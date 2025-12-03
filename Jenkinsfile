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
                    echo "Current directory:"
                    sh 'pwd'
                    echo "Listing files:"
                    sh 'ls -la'
                    echo "Full tree:"
                    sh 'ls -R'
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Package version: ${appVersion}"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}