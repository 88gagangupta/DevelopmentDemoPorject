pipeline {
  agent any
  stages {
    stage('RunDevelopmentProjectBuild') {
      steps {
        bat 'd: & cd D:\\Tx_Automate\\DevelopmentDemoPorject & mvn package'
      }
    }
    stage('Code Analysis') {
      steps {
        bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn sonar:sonar -Dsonar.host.url=http://localhost:9000'
      }
    }
    stage('RunAutomationTests_API') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
        bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn test -Dcucumber.options="--tags @APItests"'
        }
      }
    }
  }
}
