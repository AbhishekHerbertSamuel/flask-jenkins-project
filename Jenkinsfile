pipeline {
    agent {
        docker { image 'node:alpine' } // Use a lightweight Node.js Docker image
    }

    environment {
        APP_NAME = "NodeJS Jenkins App"
        APP_VERSION = "1.0.0"
    }

    stages {
        stage('Display Environment Variables') {
            steps {
                script {
                    echo "🔹 Application Name: ${APP_NAME}"
                    echo "🔹 Application Version: ${APP_VERSION}"
                }
            }
        }

        stage('Setup Directory Structure') {
            steps {
                sh 'mkdir -p app'
                sh 'ls -l'
            }
        }

        stage('Generate Node.js File') {
            steps {
                sh 'echo "console.log(\'Hello from Node.js!\');" > app/app.js'
            }
        }

        stage('Display Directory Contents') {
            steps {
                sh 'ls -l app/'
            }
        }

        stage('Run Node.js File') {
            steps {
                sh 'node app/app.js'
            }
        }

        stage('Archive Build Output') {
            steps {
                archiveArtifacts artifacts: 'app/app.js', fingerprint: true
            }
        }
    }

    post {
        always {
            echo "📌 Cleaning up workspace..."
            cleanWs()
        }
    }
}

