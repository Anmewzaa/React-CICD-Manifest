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
        stage('Test Trigger') {
            steps {
                script {
                    env.VERSION = "${DOCKERTAG}"
                    withCredentials([usernamePassword(credentialsId: 'Github-Token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email punyakon857@gmail.com"
                        sh "git config user.name Anmewzaa"
                        sh "cat k8s/deployment.yaml | envsubst | git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Anmewzaa/React-CICD-Manifest.git HEAD:main"
                    }
                }
            }
        }
        // stage("Deploy to Kubernetes") {
        //     steps {
        //       sh('''
        //           cat k8s/deployment.yaml | envsubst | sudo kubectl apply -f -
        //           sudo kubectl apply -f k8s/service.yaml
        //           echo "Deploy Version:${VERSION}"
        //       ''')
        //     }
        // }
    }
}