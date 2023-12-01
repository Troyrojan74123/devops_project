pipeline {
    agent {
        label 'linuxslave1'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub01')
    }

    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/Troyrojan74123/devops_project'
                echo 'Git Checkout Completed' 
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t troy74123/dockerimagepush:latest .'
                echo 'Build Image Completed' 
            }
        }
        stage('Login to Docker Hub') {      	
            steps{                       	
	            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		    echo 'login successful'
	                 
                }           
        } 

        stage('Push image') {
            steps {
                sh 'sudo docker push troy74123/dockerimagepush:latest'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
