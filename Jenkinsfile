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
                script {
                    git url:'https://github.com/Dhanushamk/april-prt.git', branch:'main'
                }
            }
        }
        stage('docker') {
            steps {
                script {
                    sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                    sh 'sudo docker build /home/ubuntu/jenkins/workspace/job1/ -t dhanushamk/april-prt'                    
                    sh 'sudo docker push dhanushamk/april-prt'
                }
            }
        }
        stage('K8s') {
            steps {
                script {
                    sh 'kubectl apply -f deploy.yaml'
                    sh 'kubectl apply -f service.yaml'
                    
                }
            }
        }
    }
}
