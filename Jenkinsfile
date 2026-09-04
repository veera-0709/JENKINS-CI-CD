pipeline {
    agent any

    tools {
        maven 'mvn-3.9.16'
        jdk 'JDK-21'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(credentials: ['ec2-user']) {
            sh 'echo Deploying artifact to remote server...'
            sh 'scp -o StrictHostKeyChecking=no target/jenkinsproject1-java-1.0-SNAPSHOT.jar ubuntu@13.40.104.253:/home/ubuntu/'
            sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.40.104.253 systemctl restart jenkinsproject1'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build or Deployment Failed!'
        }
    }
}
