node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            sh '''
                    git config user.email pipe.barreto07@gmail.com
                    git config user.name FelipeBarretoB
                    git checkout main
                    cd ${NAME}
                    sed -i 's+pipebarreto/${NAME}.*+pipebarreto/${NAME}:${DOCKERTAG}+g' deployment.yml
                    echo  'Sucessfully updated deployment.yml with image: pipebarreto/${NAME}:${DOCKERTAG}'
                    cat deployment.yml
            '''
        }
    }

    stage('Validate Manifests') {
        script {
            sh '''
            cd ${NAME}
            yamllint .
            kubeval deployment.yml
            kubeval service.yml
            kubectl apply --dry-run=client -f deployment.yml
            kubectl apply --dry-run=client -f service.yml
            '''
        }
    }


    stage('push to GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh '''
                    git config user.email pipe.barreto07@gmail.com
                    git config user.name FelipeBarretoB
                    git checkout main
                    git add ${NAME}/deployment.yml
                    git pull --rebase origin main
                    git commit -m 'Done by Jenkins Job updatemanifest: ${env.BUILD_NUMBER}' || echo 'No changes to commit'
                    git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/FelipeBarretoB/ecommerce-kubernetes-manifest.git HEAD:main
                    '''
                }
            }
        }
    }
}