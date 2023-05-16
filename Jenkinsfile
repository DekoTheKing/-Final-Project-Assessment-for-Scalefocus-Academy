pipeline {
    agent any
    environment {
        KUBECONFIG = '/Users/dejan/.kube/config'
    }   
    stages {
         stage('Check or Create Namespace') {
            steps {
                script {
                    def namespace = 'wp'
                    def namespaceExists = bat(returnStatus: true, script: "kubectl get namespace ${namespace}")
                    
                    if (namespaceExists == 0) {
                        echo "Namespace '${namespace}' exists."
                    } else {
                        bat "kubectl create namespace ${namespace}"
                    }
                }
            }
        }
        
    
        stage('Check and Install WordPress') {
            steps {
                script {
                    def chartName = 'wordpress'
                    def releaseName = 'final-project-wp-scalefocus'
                    def chartInstalled = bat(
                        script: "helm list -q ${releaseName}",
                        returnStatus: true
                    )
                    
                    if (chartInstalled != 0) {
                        bat "helm install ${releaseName} /Users/dejan/Documents/GitHub/Final-Project-Assessment-for-Scalefocus-Academy/charts/bitnami/wordpress -n wp -f /Users/dejan/Documents/GitHub/Final-Project-Assessment-for-Scalefocus-Academy/charts/bitnami/wordpress/values.yaml"
                    } else {
                        echo "WordPress chart is already installed."
                    }
                }
            }
        }       
        stage('Port forwarding') {
            steps {
  
				sleep time: 60, unit: 'SECONDS'
			    bat "kubectl port-forward --namespace wp svc/final-project-wp-scalefocus-wordpress 80:80" //We have a wordpress user's blog :)
            }
        }
        
        
    }
}
