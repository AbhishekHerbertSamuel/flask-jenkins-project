pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/AbhishekHerbertSamuel/flask-jenkins-project.git'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Stop Existing Flask App') {
            steps {
                script {
                    sh 'pkill -f flask || true' // Stops any existing Flask instance
                }
            }
        }
        stage('Run Flask Application') {
            steps {
                sh '. venv/bin/activate && python app.py &'
            }
        }
        stage('Verify Flask App') {
            steps {
                script {
                    sh 'curl -I http://127.0.0.1:5000 || exit 1'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.py', fingerprint: true
            }
        }
    }
}
