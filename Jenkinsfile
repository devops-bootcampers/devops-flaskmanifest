pipeline {
  agent any
  stages {
    stage('Cloning / Git') {
      steps {
        git(credentialsId: 'github', url: 'https://github.com/devops-bootcampers/flaskmanifest.git', branch: 'master', poll: true)
      }
    }

  }
}