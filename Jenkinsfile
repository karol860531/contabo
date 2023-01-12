pipeline {
    agent any

    stages {
        stage('Verify_branch_name') {

stage('Build-Docker-Image') {
      steps {
        container('docker') {
          sh 'docker build -t ss69261/testing-image:latest .'
        }
      }
    }
    }
}}


