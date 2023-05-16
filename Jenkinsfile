pipeline {
    agent any

    stages {
        stage('Check and Create Namespace') {
            steps {
                script {
                    def namespaceExists = sh(script: 'kubectl get namespace wp --no-headers --output=go-template="{{.metadata.name}}"', returnStdout: true).trim()

                    if (namespaceExists.empty) {
                        sh 'kubectl create namespace wp'
                    }
                }
            }
        }

        stage('Check and Install WordPress Chart') {
            steps {
                script {
                    def chartExists = sh(script: 'helm ls --short -n wp | grep -q "wordpress"', returnStatus: true)

                    if (chartExists != 0) {
                        sh 'helm install my-wordpress bitnami/wordpress --namespace wp'
                    }
                }
            }
        }
    }
}
