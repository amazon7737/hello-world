pipeline {
  agent any

  stages {
    stage('Clone Repository') {
        steps {
          git 'https://github.com/amazon7737/hello-world.git'
          }
    }
      stage('Build') {
        steps {
          echo 'Building from GitHub!'
        }

    }
  }
}
