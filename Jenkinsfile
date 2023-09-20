pipeline {
  agent any
  
  environment {
    AUTHOR = "Airist Kara"
    EMAIL = "eairist@gmail.com"
  }

  stages {
    stage("OS Setup") {
      matrix {
        axes {
          axis {
            name "OS"
            values "linux", "windows", "mac"
          }
          axis {
            name "ARC"
            values "32", "64"
          }
        }
        excludes {
          exclude {
            axis {
              name "OS"
              values "mac"
            }
            axis {
              name "ARC"
              values "32"
            }
          }
        }
        stages {
          stage("OS Setup") {
            agent  {
              node {
                label "linux && java11"
              }
            }
            steps {
              echo("Setup ${OS} ${ARC}")
            }
          }
        }
      }
    }

    stage("Preparation") {
      parallel {
        stage("Prepare Java") {
          agent {
            node {
              label "linux && java11"
            }
          }
          steps {
            echo("Prepare Java")
            sleep(5)
          }
        }
        stage("Prepare Linux") {
          agent {
            node {
              label "linux && java11"
            }
          }
          steps {
            echo("Prepare Maven")
            sleep(5)
          }
        }
      }
    }

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
    stage('Run PHP Artisan Test') {
      steps {
        sh 'docker compose exec app php artisan test'
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
    
    post {
    always {
      echo "I will always say Hello again!"
    }
    success {
      echo "Yay, success"
    }
    failure {
      echo "Oh no, failure"
    }
    cleanup {
      echo "Don't care success or error"
    }
  }
}