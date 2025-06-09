def services = [
  [name: 'api-gateway', path: 'api-gateway', dockerfile: 'api-gateway/Dockerfile'],
  [name: 'user-service', path: 'user-service', dockerfile: 'user-service/Dockerfile'],
  [name: 'product-service', path: 'product-service', dockerfile: 'product-service/Dockerfile'],
  [name: 'favourite-service', path: 'favourite-service', dockerfile: 'favourite-service/Dockerfile'],
  [name: 'order-service', path: 'order-service', dockerfile: 'order-service/Dockerfile'],
  [name: 'shipping-service', path: 'shipping-service', dockerfile: 'shipping-service/Dockerfile'],
  [name: 'payment-service', path: 'payment-service', dockerfile: 'payment-service/Dockerfile'],
  [name: 'proxy-client', path: 'proxy-client', dockerfile: 'proxy-client/Dockerfile']

]


pipeline {
  agent any
  parameters {
    string(name: 'DOCKERTAG', defaultValue: '', description: 'Docker image tag to deploy')
  }
  environment {
    REGISTRY = "pipebarreto"
}
  stages {
    stage('Update Manifests') {
      steps {
        script {
          services.each { svc ->
            sh """
              sed -i "s|image: $REGISTRY/${svc.name}:.*|image: $REGISTRY/${svc.name}:${DOCKERTAG}|" ${svc.manifest}
            """
            // Optionally commit the change
            sh """
              git config user.email pipe.barreto07@gmail.com
              git config user.name FelipeBarretoB
              git add ${svc.manifest}
              git commit -m "ci: update ${svc.name} image tag to ${DOCKERTAG}" || echo "No changes to commit"
              git push || echo "No remote push"
            """
          }
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        script {
          services.each { svc ->
            sh "kubectl apply -f ${svc.manifest}"
          }
        }
      }
    }
  }
}