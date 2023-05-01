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
    stage('argocd repository update') {
      steps {
      sh '''
	 
         git clone https://github.com/coldpaper2/jenkins-argocd-cd
         sed s/nginx:1.17/nginx:1.18/g jenkins-argocd-cd/argo/deploy.yaml
         git add .
	 git commit -m "${DOCKER_IMAGE_NAME}"
         git remote add https://github.com/coldpaper2/jenkins-argocd-cd.git
         git push origin main
      '''
      }

    }

    


}


}


