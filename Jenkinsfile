pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''echo PATH=${PATH}
echo M2_HOME=${M2_HOME}'''
        sh 'git url: \'https://github.com/jglick/simple-maven-project-with-tests.git\''
        sh '${M2_HOME}/bin/mvn clean'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
    }
    stage('Report') {
      steps {
        junit 'target/surefire-reports/**/*.xml'
        archiveArtifacts 'target/*.jar,target/*.hpi'
      }
    }
  }
}