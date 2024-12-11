pipeline{
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }
  }
  stages {
    stage('maven version'){
      steps{
        sh(script: 'mvn --version')
      }
      post{
          always{
            echo(message: 'maven version stage ')
          }
      }
    }
    stage('validation'){
      steps{
        sh(script: 'mvn validate')
      }
      post{
          always{
            echo(message: 'maven validations stage ')
          }
          success{
            echo(message: 'maven validations successfull')
          }
          unsuccessful{
            echo(message: 'maven validations unsuccessfull')
          }
      }
    }

    stage('Test'){
      steps{
        sh 'mvn test'
      }
      post{
          always{
            echo(message: 'maven Test stage ')
          }
          success{
            echo(message: 'maven test successfull')
          }
          unsuccessful{
            echo(message: 'maven test unsuccessfull')
          }
      }
    }
    stage('Build'){
      steps{
        sh 'mvn -B -DskipTests clean package'
      }
      post{
          always{
            echo(message: 'maven Build stage ')
          }
          success{
            echo(message: 'maven Build successfull')
            archive '**/target/*.jar'
          }
          unsuccessful{
            echo(message: 'maven Build unsuccessfull')
          }
      }
    }
    stage('Build docker image'){
      steps{
        script{
              sh 'docker build -t jenkins/my-app-1.0-SNAPSHOT .'
            }
        }
    }
      
  }
}

