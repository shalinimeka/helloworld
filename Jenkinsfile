pipeline {
  agent any
  tools { 
      maven 'MAVEN_HOME' 
      jdk 'JAVA_HOME' 
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/shalinimeka/helloworld.git'
      }
    }
    stage('Pull Changes') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('Build') {
      steps {
        echo '<--------------- Building --------------->'
        sh 'printenv'
        sh 'mvn -B -ntp -Dmaven.test.failure.ignore verify'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        sh 'mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
    stage("Deploy") {
          steps {
              script {
                 deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://localhost:8090')], contextPath: '/pipeline', onFailure: false, war: 'webapp/target/*.war' 
              }
          }
      }

}
}
