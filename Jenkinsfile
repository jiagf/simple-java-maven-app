pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('BuildTotal') {
      parallel {
        stage('Build') {
          agent {
            docker {
              image 'maven:3-alpine'
              args '-v /root/.m2:/root/.m2'
            }

          }
          steps {
            sh 'mvn -B -DskipTests clean package'
          }
        }
        stage('outputP') {
          steps {
            echo 'Build end'
          }
        }
      }
    }
    stage('test') {
      steps {
        sh 'mvn test'
        junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true)
      }
    }
  }
}