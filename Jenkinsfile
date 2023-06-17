pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'TAG=main_${BUILD_NUMBER}'
                sh 'docker build -t hkccr.ccs.tencentyun.com/myapp/publicmyapp:main_${BUILD_NUMBER} .'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    sh 'docker login  hkccr.ccs.tencentyun.com --username=$DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                    sh 'docker push hkccr.ccs.tencentyun.com/myapp/publicmyapp:main_${BUILD_NUMBER}'
                }
            }
        }
    }
}
