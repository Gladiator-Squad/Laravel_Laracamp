pipeline {
  agent any
  stages {
    stage("Verify Tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker compose version 
          curl --version
          jq --version
        '''
      }
    }
    stage('Build Image App') {
      steps {
        sh 'docker compose build app'
        sh 'docker compose up -d --no-color --wait'
        sh 'docker compose ps'
      }
    }
    stage('Remove Package Laravel') {
      steps {
        sh 'docker compose exec app rm -rf vendor composer.lock'
      }
    }
    stage('Install Package Composer.json') {
      steps {
        sh 'docker compose exec app composer install'
      }
    }
    stage('Container Generate Key & Migrations') {
      steps {
        sh 'docker compose exec app php artisan key:generate'
        sh 'docker compose exec app php artisan migrate:refresh --seed'
      }
    }
    stage('Run tests against the container') {
      steps {
        sh 'curl http://localhost:8000'
      }
    }
    stage('Deliver') {
          steps {
              input message: 'Finished using the website? (Click "Proceed" to continue)'
              sh 'docker compose down'
              sh 'docker compose ps'
          }
      }
  }
}