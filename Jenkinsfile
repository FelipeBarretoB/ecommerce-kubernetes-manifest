node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh """
                    git config user.email pipe.barreto07@gmail.com
                    git config user.name FelipeBarretoB
                    git checkout main
                    cd ${NAME}
                    sed -i 's+pipebarreto/${NAME}.*+pipebarreto/${NAME}:${DOCKERTAG}+g' deployment.yml
                    echo  'Sucessfully updated deployment.yml with image: pipebarreto/${NAME}:${DOCKERTAG}'
                    cat deployment.yml
                    git add .
                    git commit -m 'Done by Jenkins Job updatemanifest: ${env.BUILD_NUMBER}'
                    git push @github.com/${GIT_USERNAME}/ecommerce-kubernetes-manifest.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ecommerce-kubernetes-manifest HEAD:main"
                    """
                }
            }
        }
    }
}