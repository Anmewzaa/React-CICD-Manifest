pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout from SCM') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Github-token', url: 'https://github.com/Anmewzaa/React-CICD-Manifest']])
            }
        } 
        stage('Update kubernetes manifest file') {
            steps {
                sh('''
                    sudo sed -i "s/v0.0.*/${DOCKERTAG}/g" k8s/deployment.yaml
                    cat k8s/deployment.yaml
                ''')
            }
        }
    }
}