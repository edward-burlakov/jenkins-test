pipeline {
  agent {
    docker {
      alwaysPull true
      image 'alainchiasson/docker-molecule'
      args '--privileged -v /DATA/docker-cache:/docker-cache'
    }
  }
  stages {
    stage ("Docker install") {
       steps {
         sh 'yum check-update'
         sh 'curl -fsSL https://get.docker.com/ | sh'
         sh 'sudo systemctl start docker'
         sh 'sudo systemctl enable docker'
         sh 'sudo systemctl status docker'
         sh 'sudo usermod -aG docker $(whoami)'
       }
    }
    stage ("Display environment info") {
      steps {
        sh 'env'
      }
    }
    stage ("Display Molecule version") {
      steps {
        sh 'molecule --version'
      }
    }
    stage ("Validate Docker."){
      steps {
        sh 'docker info'
      }
    }
    stage ("Validate Tests Pass."){
      steps {
        sh 'cd sample && molecule test'
      }
    }
  }
}