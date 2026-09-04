pipeline {
  agent any

  tools {
    maven 'Maven-3.9'
    jdk 'JDK-17'
  }

  stage {

    stage ('Build') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('package') {
      steps {
        sh 'mvn package'
      }
    }
  }

  post {
    success {
      echo 'Build successful!'
    }
    failure {
      echo '  Build failed!'
    }
  }
}
