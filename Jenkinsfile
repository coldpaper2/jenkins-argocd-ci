pipeline {

  agent any


  stages {

    stage('docker build & push') {
      steps {
        git url: 'https://github.com/coldpaper2/jenkins-argocd-ci.git', branch: 'main'
        withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD')])   {

        sh "docker login --username=${DOCKER_USER_ID} --password=${DOCKER_USER_PASSWORD}"
        sh '''
	   docker build -t ${DOCKER_UESR_ID}:jenkins-argocd:v1 .
           docker push ${DOCKER_UESR_ID):jenkins-argocd:v1 
        '''
      }

      }

    }


}






}
