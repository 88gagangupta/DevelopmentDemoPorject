pipeline {
  agent any
  stages {
    stage('RunDevelopmentProjectBuild') {
      steps {
        bat 'd:'
        bat 'cd D:\\Tx_Automate\\DevelopmentDemoPorject'
        bat 'mvn package'
      }
    }
    stage('RunAutomationTests_API') {
      steps {
        bat 'd:'
        bat ' cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0'
        bat 'mvn test -Dcucumber.options="--tags @APItests"'
        junit(testResults: '\\target\\surefire-reports\\junitreports\\*.xml', healthScaleFactor: 1)
      }
    }
  }
}