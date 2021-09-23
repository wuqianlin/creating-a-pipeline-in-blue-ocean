pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('build ap') {
      parallel {
        stage('Build') {
          steps {
            sh 'npm install'
          }
        }

        stage('build bp') {
          steps {
            sh 'echo "build bp"'
          }
        }

      }
    }

    stage('rename image') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('checksum') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

    stage('checkmd5') {
      steps {
        sh 'echo "checkmd5"'
      }
    }

    stage('upload') {
      steps {
        sh 'echo "upload"'
      }
    }

  }
}