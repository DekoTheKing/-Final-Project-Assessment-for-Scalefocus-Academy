pipeline {
    agent any

    environment {
        CHART_NAME = 'final-project-wp-scalefocus'
        RELEASE_NAME = 'my-wordpress'
        CHART_PATH = '/Users/dejan/Documents/GitHub/Final-Project-Assessment-for-Scalefocus-Academy/bitnami/wordpress/Chart.yaml'
        VALUES_FILE = '/Users/dejan/Documents/GitHub/Final-Project-Assessment-for-Scalefocus-Academy/charts/bitnami/wordpress/values.yaml'
        NAMESPACE = 'wp'
        KUBECONFIG = '/Users/dejan/.kube/config'
        HELM_PATH = '/ProgramData/chocolatey/bin/helm.exe'
    }

    stages {
        stage('Check and Create Namespace') {
            steps {
                script {
                    def namespaceExists = bat(
                        script: "kubectl --kubeconfig %KUBECONFIG% get namespace %NAMESPACE% --no-headers --output=go-template=\"{{.metadata.name}}\"",
                        returnStdout: true
                    ).trim()

                    if (namespaceExists.empty) {
                        bat "kubectl --kubeconfig %KUBECONFIG% create namespace %NAMESPACE%"
                    }
                }
            }
        }

        stage('Deploy WordPress Chart') {
            steps {
                script {
                    def chartExists = bat(
                        script: "%HELM_PATH% list -n %NAMESPACE% --short | findstr /C:\"%RELEASE_NAME%\"",
                        returnStdout: true
                    ).trim()

                    if (chartExists.empty) {
                        bat "%HELM_PATH% install %RELEASE_NAME% %CHART_PATH% --values %VALUES_FILE% --namespace %NAMESPACE% --set nameOverride=%CHART_NAME% --kubeconfig %KUBECONFIG%"
                    } else {
                        bat "%HELM_PATH% upgrade %RELEASE_NAME% %CHART_PATH% --values %VALUES_FILE% --namespace %NAMESPACE% --set nameOverride=%CHART_NAME% --kubeconfig %KUBECONFIG%"
                    }
                }
            }
        }
    }
}
