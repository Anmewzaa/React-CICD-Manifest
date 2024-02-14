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
        stage('Update Deployment Manifest') {
            steps {
                sh 'sed "s/{{GIT_COMMIT}}/$GIT_COMMIT/g" ../../deployment.yaml > ./deployment.yaml'
            }
        }
        stage("test") {
            steps {
                script {
                    sh('''
                        sed -i "s/replaceImageTag/${DOCKERTAG}/g" k8s/deployments.yaml
                        cat k8s/deployments.yaml
                    ''')
                }
            }
        }
        // stage('Commit & Push to Gitops Repo') {
        //     steps {
        //         script {
        //             sh('''
        //                 git config --global user.email 'Punyakon857@gmail.com'
        //                 git config --global user.name 'Anmewzaa'
        //                 git remote set-url origin https://$Github-Token@github.com/Anmewzaa/React-CICD-Manifest.git
        //                 git checkout main
        //                 git add k8s/deployment.yaml
        //                 git commit -am "Updated Deployment.yaml"
        //                 cat deployment.yaml
        //                 git push origin main
        //             ''')
        //         }
        //     }
        // }
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