pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        sh './mvnw package'
      }
    }

    stage('qualitie') {
      steps {
        sh '''./mvnw checkstyle:checkstyle

./mvnw pmd:check'''
      }
    }

  }
}