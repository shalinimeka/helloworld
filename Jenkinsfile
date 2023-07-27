pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/sonupathak1/helloworld.git'
      }
    }
    stage('Pull Changes') {
      steps {
        bat 'git pull origin main'
      }
    }
    stage('Build') {
      steps {
        echo '<--------------- Building --------------->'
        bat 'printenv'
        bat 'mvn clean install'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        bat 'mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
    stage("Scan") {
          steps {
              withSonarQubeEnv(installationName: 'sonarqube_token') {
                 bat 'mvn clean verify sonar:sonar'
              }
          }
      }

}
}
