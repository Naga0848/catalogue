pipeline {
    agent {
        label 'AGENT-1'
    }
     environment { 
        appVersion = ''
        REGION = "us-east-1"
        ACC_ID = "843303282697"
     }
     options {
            timeout(time: 30, unit: 'MINUTES') 
            disableConcurrentBuilds()
            ansiColor('xterm')
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
        stage('Docker Build') {
            steps {
                sh """
                    aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .
                    docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                    #aws ecr wait image-scan-complete --repository-name ${PROJECT}/${COMPONENT} --image-id imageTag=${appVersion} --region ${REGION}
                """
            }
        }
    }
}