pipeline{
  agent {
  docker{
    image 'maven:3-alpine'
    args '-v /root/.m2:/root/.m2'
    }
  }
  
  stages{
  stage('build'){
    steps {
      bat 'mvn clean package'
    }
  }
  stage('test'){
    steps {
      bat 'mvn test'
    }
     post{
    always {
    junit 'target/surefire-reports/*.xml'
      }
    }
  }
}
}