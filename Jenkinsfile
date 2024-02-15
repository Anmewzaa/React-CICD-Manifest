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
        stage('Update Git') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Github-Token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email punyakon857@gmail.com"
                        sh "git config user.name Anmewzaa"
                        sh "git add ."
                        sh "git commit -m 'Update deployment.yaml'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/React-CICD-Manifest.git HEAD:main"
                }
            }
        }
    }
}