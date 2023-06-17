pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'VERSION=main-${BUILD_NUMBER}'
                sh 'docker-compose build -e VERSION=${VERSION}' 
                sh 'echo version= $VERSION'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    sh 'docker login  hkccr.ccs.tencentyun.com --username=$DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                    sh 'docker tag myapp-web hkccr.ccs.tencentyun.com/myapp/publicmyapp:v0.0.2'
                    sh 'docker push hkccr.ccs.tencentyun.com/myapp/publicmyapp:v0.0.2'
                }
            }
        }
    }
}
