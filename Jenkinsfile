pipeline {
  agent any
  stages {
    stage('Test & Build') {
      agent {
        node {
          label 'zouktil'
        }

      }
      steps {
        sh '''mvn -Dmaven.test.failure.ignore clean package
'''
        stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'zouktil'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}