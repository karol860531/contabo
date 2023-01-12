pipeline {
    agent {
        kubernetes {
            label "docker"
            cloud "kubernetes"
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