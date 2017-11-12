pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''echo PATH=${PATH}
echo M2_HOME=${M2_HOME}
git clone \'https://github.com/jglick/simple-maven-project-with-tests.git\'
cd simple-maven-project-with-tests
${M2_HOME}/bin/mvn clean'''
      }
    }
    stage('Build') {
      steps {
        sh '''cd simple-maven-project-with-tests
${M2_HOME}/bin/mvn -Dmaven.test.failure.ignore=true install'''
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