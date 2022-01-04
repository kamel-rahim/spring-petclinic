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

        stage('') {
          steps {
            sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=PetClinic \\
  -Dsonar.host.url=http://sonarqube \\
  -Dsonar.login=c5b26c41b2fe29a1b3e3649bcabc6ad984f60353'''
          }
        }

      }
    }

  }
}