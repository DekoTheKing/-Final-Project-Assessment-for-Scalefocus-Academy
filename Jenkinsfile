pipeline {
    agent any
    
    stages {
        stage('Check and Create Namespace') {
            steps {
                script {
                    def namespace ='wp'
                    def namespaceExists = false
                    
                    try {
                        sh(returnStdout: true, script: "kubectl get namespaces ${namespace} | grep -w ${namespace}").trim()
                        namespaceExists = true
                    } catch (Exception e) {
                        echo "Namespace $namespace does not exist."
                    }
                    
                    if (namespaceExists) {
                        echo "Namespace $namespace already exists."
                    } else {
                        echo "Namespace $namespace does not exist. Creating..."
                        sh "kubectl create namespace $namespace"
                    }
                }
            }
        }
    }
}
