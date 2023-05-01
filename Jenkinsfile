pipeline {

  agent any


  stages {

    stage('docker build & push') {
      steps {
        withCredentials([dockerhub-crendential( credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD')])   {

        sh "docker login --username=${DOCKER_USER_ID} --password=${DOCKER_USER_PASSWORD}"
      }

        sh '''
          "docker build -t mhkim1560:jenkinsargocd:v1 . "
          "docker push ${DOCKER_USER_ID}:jenkinsargocd:v1 "
        '''
      }

    }


}






}
