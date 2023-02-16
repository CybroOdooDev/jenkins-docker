pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn package'
                script {
                    docker.build("my-image:${BUILD_NUMBER}")
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    docker.image("my-image:${BUILD_NUMBER}")
                          .withRun("-p 8080:8080") {
                              sh 'java -jar target/my-app.jar'
                          }
                }
            }
        }
    }
}
