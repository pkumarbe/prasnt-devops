pipeline {
    agent { label 'node1' }
    environment {
        command_to_execute = "docker run --name my-devops-custom-web -d my-scm-web:0.0.${BUILD_NUMBER}"
       }

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
	        	sh 'docker tag  my-scm-web:0.0.${BUILD_NUMBER} docker.io/pk1dockerhub/my-scm-web:0.0.${BUILD_NUMBER}'
                sh 'docker push docker.io/pk1dockerhub/my-scm-web:0.0.${BUILD_NUMBER}'
             }
            }
        }
        stage('deploy to dev'){
            
            steps{
                 sshagent(['rootn1']) {
                    sh 'echo  "${command_to_execute}"' 
                    sh 'ssh -o StrictHostKeyChecking=no root@34.123.165.202 ${command_to_execute}'
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

