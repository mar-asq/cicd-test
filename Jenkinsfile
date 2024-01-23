pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-token')
  }
  stages {
    stage('Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('Docker_image') {
      steps {
        sh 'docker build -t maraskar/image1:$BUILD_NUMBER .'
      }
    }

    stage('docker_push') {
      steps {
        sh '''echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io

docker push maraskar/image1:$BUILD_NUMBER'''
      }
    }

  }
}
