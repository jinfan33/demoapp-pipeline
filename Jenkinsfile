pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy staging') {
      steps {
        input 'Ok to deploy to production? '
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demopapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'jin.fan@gmail.com', subject: "Failed pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}