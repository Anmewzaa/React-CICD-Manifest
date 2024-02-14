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
                    sh('''
                        sed -i 'punyakon/react-pipeline-image.* punyakon/react-pipeline-image:${DOCKERTAG}+g' deployment.yaml
                        cat deployment.yaml
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