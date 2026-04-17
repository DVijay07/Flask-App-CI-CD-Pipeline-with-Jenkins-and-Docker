
pipeline {


agent any
triggers {
    githubPush()}

environment {
    IMAGE_NAME = "Flask App CI/CD Pipeline with Jenkins and Docker"
    CONTAINER_NAME = "Flask App CI/CD Pipeline with Jenkins and Docker-container"
    DOCKER = "docker"
    REPO_URL = "https://github.com/DVijay07/Flask-App-CI-CD-Pipeline-with-Jenkins-and-Docker.git"
}

stages {

    stage('Checkout Code') {
        steps {
            git branch: 'main', url: "$REPO_URL"
        }
    }

    stage('Check Docker') {
        steps {
            sh '$DOCKER --version'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh '$DOCKER build -t $IMAGE_NAME .'
        }
    }

    stage('Stop Old Container') {
        steps {
            sh '''
            $DOCKER stop $CONTAINER_NAME || true
            $DOCKER rm $CONTAINER_NAME || true
            '''
        }
    }

    stage('Run Container') {
        steps {
            sh '$DOCKER run -d -p 8081:8080 --name $CONTAINER_NAME $IMAGE_NAME'
        }
    }

}


}
