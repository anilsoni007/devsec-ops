pipeline {
  agent any
  tools {
  maven 'maven3.9.8'
}
  stages {
    stage('Checkout'){
        steps {
            git branch: 'sandbox', url: 'https://github.com/anilsoni007/devsec-ops'
        }
    }
    stage('Build Artifact - Maven') {
      steps {
        sh "mvn clean package -DskipTests=true"
        archive 'target/*.jar'
      }
    }
    stage('Unit Tests - JUnit and Jacoco') {
      steps {
        sh "mvn test"
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }
  }
}
