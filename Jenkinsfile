pipeline {
  agent any

  environment {
    def myLink = 'https://github.com/BiggansFot/fooproject.git'
    def myBuild = 'mvn compile'
    def myTest = 'mvn test'
    def postAlways = '**/TEST*.xml'
  }
  parameters {
    booleanParam(defaultValue: false, description: "Enable service?", name: 'myBoolean')
  }

  stages {
    stage('Checkout') {
      steps {
        git "${myLink}"
      }
    }
    stage('Build') {
      steps {
        bat "mvn compile"
      }
    }  
    stage('Test') {
      steps {
        bat "mvn test"
      }
      post {
        always {
          jacoco {
            execPattern: 'target/*.exec',
            classPattern: 'target/classes',
            sourcePattern: 'src/main/java',
            exclusionPattern: 'src/test*'
          }
          junit '**/TEST*.xml'
        }
      }
    }
  }
}