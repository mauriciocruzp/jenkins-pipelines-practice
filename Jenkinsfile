pipeline {
  agent any

  environment {
    DOCKERIMAGE = "pipeline-hello-world"
  }

  stages {
    stage ('Build') {
      steps {
        script {
          docker.build(DOCKERIMAGE)
        }
      }
    }

    stage ('Test') {
      steps {
        script {
          docker.image(DOCKERIMAGE).inside {
            sh 'npm install --loglevel=verbose'
            sh 'npm test'
          }
        }
      }
    }
    stage ('Deploy') {
      steps {
        script {
          docker.image(DOCKERIMAGE).run('-d -p 3000:3000')
        }
      }
    }
  }
}
