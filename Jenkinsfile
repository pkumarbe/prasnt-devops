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
                withCredentials([string(credentialsId:'mydockerhub', variable: 'mydockerhub')]) {
                sh 'docker login -u pkumarbe -p ${mydockerhub}'
             }
            }
        }
    }
}
