pipeline {
agent any
environment
{
FLASK_APP =
'app.py'
FLASK_PORT
= '5000'
VENV_DIR
= 'venv'
}
stages {
stage('Checko
ut Code') {
steps {
script {
git
branch: 'main',
url:
'https://github
.com/Abhishe
kHerbertSam
uel/flask-
jenkins-
project.git'
}
}
}
stage('Setup
Python
Environment')
{
steps {
sh '''
if [ ! -d
"$VENV_DIR"
]; then
python3 -m
venv
$VENV_DIR
fi
source
$VENV_DIR/bi
n/activate
pip
install --
upgrade pip
pip
install -r
requirements.
txt
'''
}
}
stage('Stop
Existing Flask
App') {
steps {
sh '''
FLASK_PID=$(
lsof -t -
i:$FLASK_POR
T)
if [ ! -z
"$FLASK_PID"
]; then
echo
"Stopping
existing Flask
app..."
kill -
9 $FLASK_PID
fi
'''
}
}
stage('Run
Flask
Application') {
steps {
sh '''
source
$VENV_DIR/bi
n/activate
nohup
python3
$FLASK_APP >
flask.log 2>&1
&
'''
}
}
stage('Verify
Flask App') {
steps {
sh '''
sleep 5
curl -I
http://127.0.0.
1:$FLASK_PO
RT || echo
"Flask App is
not running!"
'''
}
}
}
post {
always {
archiveArtifact
s artifacts:
'flask.log',
fingerprint:
true
}
}
}
