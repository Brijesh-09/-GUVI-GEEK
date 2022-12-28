pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "brijeshkori/flask"
        CONTAINER_NAME = "flask-container"
        STUB_VALUE = "200"
        registryCredential = 'brijeshkori'
    }
    stages {
        stage('Stubs-Replacement'){
            steps {
                // 'STUB_VALUE' Environment Variable declared in Jenkins Configuration 
                echo "STUB_VALUE = ${STUB_VALUE}"
            }
        }
        stage('Build') {
            steps {
                //  Building new image
                sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
                sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'

               

                    }
                } 
        stage('Deploy') {
            steps {
                script{
                     //  Pushing Image to Repository
             withCredentials([string(credentialsId: 'brijeshkori', variable: 'dockerhubpwd')]) {
              sh 'docker login -u brijeshkori -p ${dockerhubpwd}'
                }
                 sh 'docker push brijeshkori/flask:latest'
            }
        }
    }    
        
    }
}
