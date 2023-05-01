pipeline {

  agent any


  stages {

    stage('docker build & push') {
      steps {
        withCredentials([usernameColonPassword, credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD'])   {

        sh "docker login -u ${DOCKER_USER_ID} -p ${DOCKER_USER_PASSWORD}"
      }


        sh '''
          docker build -t mhkim1560:jenkinsargocd:v1 .
          docker push ${DOCKER_USER_ID}:jenkinsargocd:v1
        '''
      }

    }


}






}
