pipeline {
  agent any
  stages {
    stage('Cloning / Git') {
      steps {
        git(credentialsId: 'github', url: 'https://github.com/devops-bootcampers/flaskmanifest.git', branch: 'master', poll: true)
      }
    }

    stage('Properties') {
      steps {
        script {
          properties([parameters([string('DOCKER_TAG')])])
        }

      }
    }

    stage('Update manifest') {
      steps {
        script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
              sh "git config user.email chielvis01@gmail.com"
              sh "git config user.name chielvis01"
              //sh "git switch master"
              sh "cat deployment.yaml"
              sh "sed -i 's+chielvis1/flask:*+chielvis1/flask:${DOCKER_TAG}+g' deployment.yaml"
              sh "cat deployment.yaml"
              sh "git add ."
              sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
              sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/devops-bootcampers/flaskmanifest.git HEAD:master"
            }
          }
        }

      }
    }

    stage('echo tag') {
      steps {
        sh 'echo ${DOCKER_TAG}'
      }
    }

  }
}