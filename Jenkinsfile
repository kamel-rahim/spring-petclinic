pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        sh './mvnw package'
      }
    }

    stage('qualitie') {
      parallel {
        stage('qualitie') {
          steps {
            sh '''./mvnw checkstyle:checkstyle

./mvnw pmd:check'''
          }
        }

        stage('Sonar') {
          steps {
            sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=PetClinic'
          }
        }

      }
    }

  }
}