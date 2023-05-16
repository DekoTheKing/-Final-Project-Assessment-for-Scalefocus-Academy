def CHART_NAME = 'final-project-wp-scalefocus'
def RELEASE_NAME = 'my-wordpress'
def CHART_PATH = 'C:\Users\dejan\Documents\GitHub\Final-Project-Assessment-for-Scalefocus-Academy\charts\bitnami\wordpress/Chart.yaml'
def VALUES_FILE = 'C:\Users\dejan\Documents\GitHub\Final-Project-Assessment-for-Scalefocus-Academy\charts\bitnami\wordpress/values.yaml'
def NAMESPACE = 'wp'
def KUBECONFIG = 'C:/Users/dejan/.kube/config'
def HELM_PATH = 'C:/ProgramData/chocolatey/bin/helm.exe'

pipeline {
    agent any
    environment {
        CHART_NAME_ENV = CHART_NAME
        RELEASE_NAME_ENV = RELEASE_NAME
        CHART_PATH_ENV = CHART_PATH
        VALUES_FILE_ENV = VALUES_FILE
        NAMESPACE_ENV = NAMESPACE
        KUBECONFIG_ENV = KUBECONFIG
        HELM_PATH_ENV = HELM_PATH
    }
    stages {
        stage('Check and Create Namespace') {
            steps {
                script {
                    def namespaceExists = sh(script: "kubectl --kubeconfig \$KUBECONFIG_ENV get namespace \$NAMESPACE_ENV --no-headers --output=go-template=\"{{.metadata.name}}\"", returnStdout: true).trim()

                    if (namespaceExists.isEmpty()) {
                        sh "kubectl --kubeconfig \$KUBECONFIG_ENV create namespace \$NAMESPACE_ENV"
                    }
                }
            }
        }

        stage('Deploy WordPress Chart') {
            steps {
                script {
                    def chartExists = sh(script: "\$HELM_PATH_ENV list -n \$NAMESPACE_ENV --short | grep -q \$RELEASE_NAME_ENV && echo true || echo false", returnStdout: true).trim()

                    if (chartExists == 'false') {
                        sh "\$HELM_PATH_ENV install \$RELEASE_NAME_ENV \$CHART_PATH_ENV --values \$VALUES_FILE_ENV --namespace \$NAMESPACE_ENV --set nameOverride=\$CHART_NAME_ENV --kubeconfig \$KUBECONFIG_ENV"
                    } else {
                        sh "\$HELM_PATH_ENV upgrade \$RELEASE_NAME_ENV \$CHART_PATH_ENV --values \$VALUES_FILE_ENV --namespace \$NAMESPACE_ENV --set nameOverride=\$CHART_NAME_ENV --kubeconfig \$KUBECONFIG_ENV"
                    }
                }
            }
        }
    }
}
