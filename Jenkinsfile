pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/venuchowgani/orderapp.git',
                    branch: 'main'
                }
        }
        stage ('Build and push docker image') {
            steps {
                sh "docker image build -t venuchowgani:dev_${BUILD_ID}"
                sh "docker image push venuchowgani:dev_${BUILD_ID}"
            }
        }
        
    }
}