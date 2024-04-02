node {
    def app
    
    env.IMAGE = 'mitchxxx/bluegreen-rollout'

    stage('Clone repo'){
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github-mitchel', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        sh "git config user.email megboko@gmail.com"
                        sh "git config user.name mitchxxx"
                        //sh "git switch master"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job Rolloutmanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argo-rollout-manifests.git HEAD:main"
                }
            }
        }
    }
}
