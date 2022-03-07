pipeline {
 agent any
 tools {
 maven "maven383"
 jdk "jdk11"
 }

 stages {
 stage('Initialize'){
 steps{
 echo "PATH = ${M2_HOME}/bin:${PATH}"
 echo "M2_HOME = /opt/maven"
 }
 }
 stage('Test') {
 steps {
 bat 'mvn test'
 }

 }
 stage('Build') {
 steps {
 bat 'mvn package'
 }

 }
 stage('SonarQube Analysis') {
 steps {
 sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=testProject \                                               
  -Dsonar.host.url=http://localhost:9000 \                                       
  -Dsonar.login=test'
 }
 }

 }
 post {
 success {
 junit '**/target/*-reports/*.xml'


 }
 always {
 junit(
 allowEmptyResults: true,
 testResults: '**/target/surefire-reports/.xml'
 )
 }
 }
}