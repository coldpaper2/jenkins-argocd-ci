pipeline {

  agent any

  environment {

    DOCKER_IMAGE_NAME = "mhkim1560/jenkins-argocd"
    TAG = "v1"

  }

  stages {

    stage('docker login') {
      steps {
        withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD')])   {

        sh '''
           docker login --username=${DOCKER_USER_ID} --password=${DOCKER_USER_PASSWORD}
        '''
      }

      }
}
    stage('docker build & push') {
      steps {
      sh '''
           docker build -t ${DOCKER_IMAGE_NAME}:${TAG} .
           docker push ${DOCKER_IMAGE_NAME}:${TAG}
      '''   
    }


    }


}


}


