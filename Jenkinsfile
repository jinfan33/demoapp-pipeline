pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demp-app'
        sh '''sh run_build_script.sh
'''
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux Tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run Windows Tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        input 'ok to deploy to prod'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
}