pipeline {

  agent any

  environment {

    DOCKER_IMAGE_NAME = "mhkim1560/jenkins-argocd"

  }

  stages {

    stage('docker login') {
      steps {
        withCredentials([usernamePassword( credentialsId: 'coldpaper2-dockerhub', usernameVariable: 'DOCKER_USER_ID', passwordVariable: 'DOCKER_USER_PASSWORD')])   {

        sh '''
           docker login --username=${DOCKER_USER_ID} --password=${DOCKER_USER_PASSWORD}
        '''
      }

      }
}
    stage('docker build & push') {
      steps {
      sh '''
           docker build -t ${DOCKER_IMAGE_NAME}:${BUILD_NUMBER} .
           docker push ${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}
      '''   
    }
}
    stage('argocd repository update') {
      steps {
         git url: 'git@github.com:coldpaper2/jenkins-argocd-cd.git', credentialsId: 'jenkins-ssh', branch: 'main'
      sh '''
         pwd
         cd argo
         #yq e --inplace ".spec.template.spec.containers[0].image = \"${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}\"" deploy.yaml
         yq e --inplace '.spec.template.spec.containers[0].image = env(DOCKER_IMAGE_NAME) + ":" + env(BUILD_NUMBER)' deploy.yaml
        #cd jenkins-argocd-cd/argo
         cat deploy.yaml
	 git branch -M main
         git add .
         git commit -m "${DOCKER_IMAGE_NAME}"
         
        # git remote add origin https://github.com/coldpaper2/jenkins-argocd-cd.git
         git push origin main
				 
      '''
      }

    }

    


}


}

