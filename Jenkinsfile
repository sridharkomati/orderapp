pipeline {
    agent { label 'Docker'}
    triggers { pollSCM ('* * * * *') }
    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/sridharkomati/orderapp.git',
                    branch: 'main'
                }
        }
        stage ('Build and push docker image') {
            steps {
                sh "docker image build -t sridhar006/argo:dev_${BUILD_ID} ."
                sh "docker image push sridhar006/argo:dev_${BUILD_ID}"
            }
        }
        stage ('update k8s manifest') {
            steps {
                sh "cd ~/orderops && yq eval -i '.spec.template.spec.containers[0].image= \"sridhar006/argo:dev_${BUILD_ID}\" ' ~/orderops/manifests/orderdeploy.yaml"
                sh """
                  cd ~/orderops
                  git add ~/orderops/manifests/orderdeploy.yaml
                  git commit -m "added new change"
                  git push origin main
                """
            }
        }
        
    }
}
