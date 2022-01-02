pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        sh './mvnw package'
      }
    }

    stage('quality') {
      parallel {
        stage('quality') {
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

        stage('sonar2') {
          steps {
            withSonarQubeEnv(installationName: 'Sonar', credentialsId: 'Sonar', envOnly: true) {
              sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=PetClinic'
            }

          }
        }

      }
    }

  }
}