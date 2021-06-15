pipeline {
  agent any
  stages {
    stage('Build App') {
      steps {
    	sh 'mvn -f helloworld1 clean install'
      }
    }
    stage('Unit Test') { 
      steps {
        sh 'mvn -f helloworld1/pom.xml clean test'
      }
    }
    stage('Deploy Standalone') { 
      steps {
        sh 'mvn -f helloworld1/pom.xml deploy -P standalone'
      }
    }
    stage('Deploy ARM') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials') 
      }
      steps {
        sh 'mvn  -f helloworld1/pom.xml deploy -P arm -Darm.target.name=local-3.9.0-ee -Danypoint.username=${ANYPOINT_CREDENTIALS_USR}  -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh 'mvn  -f helloworld1/pom.xml deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
  }
}
