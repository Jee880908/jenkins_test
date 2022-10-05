pipeline {
  agent none
  stages {
    stage('Build & Test') {
      parallel {
        stage('Build & Test') {
          agent {
            node {
              label 'docker'
            }

          }
          steps {
            sh 'mvn -Dmaven.test.failure.ignore clean package'
            stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/TEST-*.xml,target/*.jar')
          }
        }

        stage('matrix1') {
          steps {
            echo 'hello'
          }
        }

        stage('matrix2') {
          steps {
            echo 'helloo'
          }
        }

      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
      }
    }

  }
}