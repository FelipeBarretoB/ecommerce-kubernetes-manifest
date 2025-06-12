node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email pipe.barreto07@gmail.com"
                    sh "git config user.name FelipeBarretoB"
                    sh "cat deployment.yml"
                    sh "sed -i 's+pipebarreto/${NAME}.*+pipebarreto/${NAME}:${DOCKERTAG}+g' deployment.yml"
                    sh "echo  'Sucessfully updated deployment.yml with image: pipebarreto/${NAME}:${DOCKERTAG}'"
                    //sh "cat deployment.yml"
                    //sh "git add ."
                    //sh "git commit -m 'Done by Jenkins Job updatemanifest: ${env.BUILD_NUMBER}'"
                    //sh "git push @github.com/${GIT_USERNAME}/jenkins-gitops-k8s.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ecommerce-kubernetes-manifest HEAD:main"
                }
            }
        }
    }
}