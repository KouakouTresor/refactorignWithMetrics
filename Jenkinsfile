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
 bat 'mvn -e clean verify sonar:sonar -Dsonar.projectKey=tuto -
Dsonar.host.url=http://localhost:9000 -Dsonar.login=f2db60c5086739c3682e78fc4e3e7ffce4a99024'
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