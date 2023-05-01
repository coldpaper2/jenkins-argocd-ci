pipeline {

  agent any


  stages {

    stage('docker build & push') {
      steps {
        withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD')])   {

        sh "docker login --username=${DOCKER_USER_ID} --password=${DOCKER_USER_PASSWORD}"
        sh "docker build -t ${DOCKER_UESR_ID}/jenkins-argocd:v1 . "
        sh "docker push ${DOCKER_UESR_ID}/jenkins-argocd:v1" 
      }

      }

    }


}






}
