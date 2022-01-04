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

        stage('error') {
          steps {
            sh '''./mvnw clean verify sonar:sonar \\
  -Dsonar.projectKey=PetClinic \\
  -Dsonar.host.url=http://sonarqube \\
  -Dsonar.login=c5b26c41b2fe29a1b3e3649bcabc6ad984f60353'''
          }
        }

        stage('sonar propre ') {
          steps {
            withSonarQubeEnv('Sonar') {
              sh '''./mvnw clean verify sonar:sonar \\
  -Dsonar.projectKey=PetClinic'''
            }

          }
        }

      }
    }

  }
}