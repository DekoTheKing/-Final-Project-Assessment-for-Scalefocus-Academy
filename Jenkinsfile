pipeline {
    agent any
    
    stages {
        stage('Check Namespace') {
            steps {
                script {
                    try {
                        def namespaceExists = sh(
                            returnStatus: true,
                            script: 'kubectl get namespace wp'
                        )
                        
                        if (namespaceExists == 0) {
                            echo 'Namespace "wp" already exists.'
                        } else {
                            echo 'Namespace "wp" does not exist. Creating...'
                            bat 'kubectl create namespace wp'
                            echo 'Namespace "wp" created successfully.'
                        }
                    } catch (Exception e) {
                        echo "Failed to check/create namespace: ${e.getMessage()}"
                        error('Failed to check/create namespace')
                    }
                }
            }
        }
        
        stage('Check WordPress') {
            steps {
                script {
                    try {
                        def wordpressExists = sh(
                            returnStatus: true,
                            script: 'kubectl get deployment -n wp | grep wordpress'
                        )
                        
                        if (wordpressExists == 0) {
                            echo 'WordPress deployment exists in namespace "wp".'
                        } else {
                            echo 'WordPress deployment does not exist in namespace "wp". Installing Helm chart...'
                            bat 'helm install final-project-wp-scalefocus /Users/dejan/Documents/GitHub/Final-Project-Assessment-for-Scalefocus-Academy/charts/wordpress-chart'
                            echo 'Helm chart installed successfully.'
                        }
                    } catch (Exception e) {
                        echo "Failed to check/install WordPress: ${e.getMessage()}"
                        error('Failed to check/install WordPress')
                    }
                }
            }
        }
    }
}
