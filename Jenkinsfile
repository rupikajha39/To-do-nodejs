pipeline {
    agent any

    environment {
        NODEJS_VERSION = '14'  // Adjust the Node.js version as needed
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git 'https://github.com/rupikajha39/To-do-nodejs'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Use nvm to install Node.js
                    tool name: "Node.js", type: "jenkins.plugins.nodejs.tools.NodeJSInstallation", installation: "${NODEJS_VERSION}"
                    sh "npm install"
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh "npm test"
                }
            }
        }

        stage('Build and Package') {
            steps {
                script {
                    sh "npm run build"
                    archiveArtifacts artifacts: 'dist/*', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
