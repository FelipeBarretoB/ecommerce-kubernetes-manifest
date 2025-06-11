def services = [
  [name: 'api-gateway', path: 'api-gateway', manifest: 'api-gateway/deployment.yml', dockerfile: 'api-gateway/Dockerfile'],
  [name: 'user-service', path: 'user-service', manifest: 'user-service/deployment.yml', dockerfile: 'user-service/Dockerfile'],
  [name: 'product-service', path: 'product-service', manifest: 'product-service/deployment.yml', dockerfile: 'product-service/Dockerfile'],
  [name: 'favourite-service', path: 'favourite-service', manifest: 'favourite-service/deployment.yml', dockerfile: 'favourite-service/Dockerfile'],
  [name: 'order-service', path: 'order-service', manifest: 'order-service/deployment.yml', dockerfile: 'order-service/Dockerfile'],
  [name: 'shipping-service', path: 'shipping-service', manifest: 'shipping-service/deployment.yml', dockerfile: 'shipping-service/Dockerfile'],
  [name: 'payment-service', path: 'payment-service', manifest: 'payment-service/deployment.yml', dockerfile: 'payment-service/Dockerfile'],
  [name: 'proxy-client', path: 'proxy-client', manifest: 'proxy-client/deployment.yml', dockerfile: 'proxy-client/Dockerfile']
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
      steps { //TODO: #5 add credentials in Jenkins
        withCredentials([string(credentialsId: 'GITHUB_TOKEN', variable: 'TOKEN')]) {
          script {
            services.each { svc ->
              sh """
                sed -i "s|image: $REGISTRY/${svc.name}:.*|image: $REGISTRY/${svc.name}:${DOCKERTAG}|" ${svc.manifest}
                git config user.email pipe.barreto07@gmail.com
                git config user.name FelipeBarretoB
                git add \${svc.manifest}
                git commit -m "ci: update ${svc.name} image tag to ${DOCKERTAG}" || echo "No changes to commit"
                git remote set-url origin https://${TOKEN}@github.com/FelipeBarretoB/ecommerce-kubernetes-manifest.git
                git push || echo "No remote push"
              """
            }
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