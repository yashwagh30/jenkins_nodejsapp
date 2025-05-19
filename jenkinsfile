pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yashwagh30/jenkins-node-demo:day60'
    }

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repo...'
                git 'https://github.com/yashwagh30/jenkins_nodejsapp'
            }
        }

        stage('Install & Test') {
            steps {
                bat 'npm install'
                bat 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat "docker login -u %DOCKER_USER% -p %DOCKER_PASS%"
                    bat "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Run Container') {
            steps {
                bat "docker run -d -p 5000:5000 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo '✅ CI/CD pipeline complete!'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}
