pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh  '$(echo ${BRANCH} |sed 's/origin\///' | sed 's/\//:/')-${BUILD_NUMBER}'
                sh 'docker-compose build'
                sh 'echo version= $VERSION'
                sh 'export VERSION=$VERSION'
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
