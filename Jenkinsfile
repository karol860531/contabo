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
                container("docker") {
                    sh "docker ps"
                }
            }
        }
    }
}