node {
    def app
    
    env.IMAGE = 'mitchxxx/bluegreen-rollout'

    stage('Clone repo'){
        git branch: 'main', url: 'https://github.com/Mitchxxx/argo-rollout-manifests.git'
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github-Mitchel', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email megboko@gmail.com"
                        sh "git config user.name mitchxxx"
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
