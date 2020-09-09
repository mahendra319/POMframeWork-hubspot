pipeline {
  agent any
  stages {
    stage('Build Dev') {
      parallel {
        stage('Build Dev') {
          steps {
            bat 'mvn clean install -DskipTests=true'
          }
        }

        stage('chrome') {
          steps {
            bat 'mvn test -Denv=dev -Dbrowser=chrome'
          }
        }

      }
    }

    stage('Build QA') {
      parallel {
        stage('Build QA') {
          steps {
            bat 'mvn clean install -DskipTests=true'
          }
        }

        stage('chrome') {
          steps {
            bat 'mvn test -Denv=qa -Dbrowser=chrome'
          }
        }

        stage('firefox') {
          steps {
            bat 'mvn test -Denv=qa -Dbrowser=firefox'
          }
        }

      }
    }

    stage('Build Stage') {
      parallel {
        stage('Build Stage') {
          steps {
            bat 'mvn clean install -DskipTests=true'
          }
        }

        stage('firefox') {
          steps {
            bat 'mvn test -Denv=stage -Dbrowser=firefox'
          }
        }

        stage('chrome') {
          steps {
            bat 'mvn test -Denv=stage -Dbrowser=chrome'
          }
        }

        stage('safari') {
          steps {
            bat 'mvn test -Denv=stage -Dbrowser=safari'
          }
        }

      }
    }

    
    stage('Publish reports') {
           steps {
                script {
                    allure([
                        includeProperties: false,
                        jdk: '',
                        properties: [],
                        reportBuildPolicy: 'ALWAYS',
                        results: [[path: '/allure-results']]
                    ])
                }
            }
        }
    
    

  }
  tools {
    maven 'M3'
  }
}