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
                    git pull --rebase origin main
                    cd ${NAME}
                    sed -i "s|image: pipebarreto/${NAME}:.*|image: pipebarreto/${NAME}:${DOCKERTAG}|g" deployment.yml
                    echo  'Sucessfully updated deployment.yml with image: pipebarreto/${NAME}:${DOCKERTAG}'
                    cat deployment.yml
            '''
        }
    }

    stage('Validate Manifests') {
        script {
            sh '''
                export PATH=$PATH:/usr/bin
                cd ${NAME}
                yamllint .
                kubeconform -strict deployment.yml
                kubeconform -strict service.yml
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
                    '''
                    sh "git commit -m 'Done by Jenkins Job updatemanifest: ${env.BUILD_NUMBER}' || echo 'No changes to commit'"
                    sh '''
                    git pull --rebase origin main
                    git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/FelipeBarretoB/ecommerce-kubernetes-manifest.git HEAD:main
                    '''
                }
            }
        }
    }
}