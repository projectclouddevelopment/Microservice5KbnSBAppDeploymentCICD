node {
    def app

    stage('Clone repository') {      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {     
                        sh "git config user.email dibs.biswas@gmail.com"
                        sh "git config user.name dibyenduBiswas"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+dibsiit123/testrepo.*+dibsiit123/testrepo:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/KubernetesApplicationManifestCICDdibs.git HEAD:main"
      }
    }
  }
}
}
