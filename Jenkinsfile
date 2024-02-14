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
        stage('Commit & Push to Gitops Repo') {
            steps {
                script {
                    sh('''
                        git config --global user.email 'Punyakon857@gmail.com'
                        git config --global user.name 'Anmewzaa'
                        git remote set-url origin https://$Github-Token@github.com/Anmewzaa/React-CICD-Manifest.git
                        git checkout main
                        git add -A
                        git commit -am "Updated Deployment.yaml"
                        cat deployment.yaml
                        git push origin main
                    ''')
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