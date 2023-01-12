pipeline {
    agent {
        kubernetes {
            inheritFrom 'docker'
        }
    }
    stages {
        stage("First") {
            steps {
                    sh "docker ps"
                
            }
        }
    }
}