node {
    def ECR_REPOSITORY_URI = 'your-ecr-repository-uri'
    stage('Clone repository') {
        checkout scm
    }

    stage('Update deployment.yaml') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email saiaunghlyanhtet2003@gmail.com"
                        sh "git config user.name saiaunghlyanhtet"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's@CONTAINER_IMAGE@${ECR_REPOSITORY_URI}:cicd-devops-gitops-${IMAGE_TAG}@' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job updatek8smanifest: ${IMAGE_TAG}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8s-manifest-cicd.git HEAD:main"
      }
    }
  }
}
}