pipeline {
    agent { label 'node1' }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('print env') {
            steps {
                sh 'env'
                sh 'whoami'
                sh 'systemctl start docker'
                sh 'sudo docker ps -a'
            }
        }
        stage('docker log in') {
            steps {
                withCredentials([string(credentialsId:'pdcokerhub', variable: 'mydockerhub')]) {
                sh 'docker login -u pk1dockerhub -p ${mydockerhub}'
                sh 'pwd'
                sh 'ls'
                sh 'docker build -t my-scm-web:0.0.${BUILD_NUMBER} .'
                sh 'docker push docker.io/pkumarbe/my-scm-web:0.0.${BUILD_NUMBER}'
             }
            }
        }
        stage('deploy to dev'){
            
            steps{
                 sshagent(['bbf5141d-4b0e-47f6-a17a-e0a37d1ec957']) {
                    // def command_to_execute="docker run --name my-devops-custom-web -d my-scm-web:0.0.${BUILD_NUMBER}"
                    sh "echo ${command_to_execute}"
                 }
         
            }
        }
    }
}


//node {
//  sshagent (credentials: ['deploy-dev']) {
//    sh 'ssh -o StrictHostKeyChecking=no -l cloudbees 192.168.1.106 uname -a'
//  }
//}

