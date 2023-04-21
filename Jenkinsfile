node {
    def app
    env.JENKINS_IP = 'http://20.228.182.157'
    stage('Clone repository') {    
        checkout scm
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email hxexx22@gmail.com"
                    sh "git config user.name YIHOEUN"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+${JENKINS_IP}:8080/onlyvictoryimg.*+${JENKINS_IP}:8080/onlyvictoryimg:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/OnlyVictory-site/gitops.git HEAD:main"
                }
            }
        }
    }
}
