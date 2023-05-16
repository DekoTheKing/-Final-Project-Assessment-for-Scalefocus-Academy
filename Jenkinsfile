pipeline {
  agent any
  environment {
    KUBECONFIG = '/Users/dejan/.kube/config'
  }
    stage('Deploymnet start') {
      steps {
        script {
          try {
            // Check if the namespace exists
            def namespaceExists = bat(script: 'kubectl get namespace default', returnStatus: true) == 0
            if (!namespaceExists) {
              // Create the namespace
              bat 'kubectl create namespace wp'
            }
            else
            {
                bat 'kubectl get services'
            }
            // Deploy the application using Helm
            bat 'helm dependency build ./bitnami/wordpress'
            bat 'helm install final-project-wp-scalefocus ./bitnami/wordpress -f ./bitnami/wordpress/values.yaml'
          } catch (Exception e) {
            error "Deployment failed: ${e.getMessage()}"
          }
        }
      }
    }
  }
}
