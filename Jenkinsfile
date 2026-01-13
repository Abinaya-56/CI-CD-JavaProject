pipeline {
    agent any

    environment {
        IMAGE_NAME = "abinaya242/java-ci-cd-demo"
        CONTAINER_NAME = "java-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                      echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                      docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/ec2-key.pem ubuntu@54.87.61.34 "
                  docker pull $IMAGE_NAME:latest &&
                  docker stop $CONTAINER_NAME || true &&
                  docker rm $CONTAINER_NAME || true &&
                  docker run -d -p 80:8080 --name $CONTAINER_NAME $IMAGE_NAME:latest
                "
                '''
            }
        }
    }
}
