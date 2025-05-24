pipeline {
    agent {
        label 'KM'
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials("dhanushamk")
    }
    stages {
        stage('git') {
            steps {
                     git url:'https://github.com/Dhanushamk/april-prt', branch:'main'
            }
        }
        stage('docker') {
            steps {
                    sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                    sh 'sudo docker build . -t dhanushamk/april-prt'                    
                    sh 'sudo docker push dhanushamk/april-prt'
            }
         }
        stage('K8s') {
            steps {
                    sh 'kubectl delete deployment my-deployment'
                    sh 'kubectl apply -f deploy.yaml'
                    sh 'kubectl apply -f service.yaml'
                    
                }
            }
        }
    }

