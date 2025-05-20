pipeline {
    agent any
    tools {
        nodejs "NodeJS" // Define this in Jenkins tools config
    }
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/yashwagh30/https://github.com/yashwagh30/jenkins_nodejsapp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
    post {
        success {
            echo '✅ All tests passed!'
        }
        failure {
            echo '❌ Some tests failed!'
        }
    }
}
