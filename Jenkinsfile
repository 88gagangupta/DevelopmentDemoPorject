pipeline {
  agent any
  stages {
    stage('RunDevelopmentProjectBuild') {
      steps {
        bat 'd:
        cd D:\\Tx_Automate\\DevelopmentDemoPorject
        mvn package'
      }
    }
    stage('RunAutomationTests_API') {
      steps {
        bat 'd: cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 mvn test -Dcucumber.options="--tags @APItests"'
        junit(testResults: 'D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0\\target\\surefire-reports\\junitreports\\*.xml', healthScaleFactor: 1)
      }
    }
  }
}
