pipeline {
  agent any
  stages {
    stage('Test Code') {
      steps {
        sh '''#/bin/bash

make test'''
      }
    }
    stage('Build') {
      parallel {
        stage('x86') {
          steps {
            sh '''#/bin/bash

docker build . -t marcoceppi/microbot'''
          }
        }
        stage('s390x') {
          steps {
            sh '''#/bin/bash

sed -i \'s/FROM nginx:alpine/FROM s390x/nginx:latest/\' Dockerfile
docker build . -t marcoceppi/microbot:latest-s390x'''
          }
        }
      }
    }
    stage('Test Image') {
      steps {
        sh '''#/bin/bash

echo "hello"'''
      }
    }
    stage('Promote') {
      steps {
        echo 'Promoting the image!'
      }
    }
  }
}