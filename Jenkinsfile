pipeline {

  agent any
  
  tools {
    maven 'maven3'
  }
  options {
    buildDiscarder logRotator(
      daysToKeepStr: '15',
      numToKeepStr: '10'
    )
  }
  environment {
     APP_NAME = "SPRING_BOOT_DEMO"
    APP_ENV = "DEV"
  }
  stages {
    stage('Cleanup Workspace') {
      steps {
        cleanWs()
      }
    }
    stage('Code Checkout') {
      steps {
        checkout([
          $class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/nishaero/spring-petclinic.git']]
        ])
      }
    }
    stage('Core Build') {
      steps {
        sh 'mvn install -Dmaven.test.skip=true'
      }
    }
    stage('Printing all Global Variables') {
      steps {
        sh """
        env
        """
      }
    }
  }
}
