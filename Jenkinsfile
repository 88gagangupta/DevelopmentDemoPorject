pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'd: & cd D:\\Tx_Automate\\DevelopmentDemoPorject & mvn package'
      }
    }

    stage('Code Analysis') {
      steps {
        bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn sonar:sonar -Dsonar.host.url=http://localhost:9000'
      }
    }

    stage('API Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn test -Dcucumber.options="--tags @APItests"'
          script{
          if(currentStage.result == 'FAILURE')
            {pipelineResult = 'FAILURE'}}
        }
      }
    }

    stage('Web Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn test -Dcucumber.options="--tags @Amazon"'
        }
      }
    }

    stage('Mobile Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          bat 'd: & cd D:\\Tx_Automate\\txautomatejava-bdd\\cucumber-jvm-template-master 2.0 & mvn test -Dcucumber.options="--tags @MobileTest"'
        }
      }
    }

    stage('Performance Test') {
      steps {
        bat 'd: && cd D:\\Tx_Automate\\ApacheJmeter\\Results && del *.* /Q && rmdir DashboardReports /S /Q'
        bat 'd: && cd D:\\Tx_Automate\\ApacheJmeter\\apache-jmeter-3.2\\bin && jmeter -n -t "D:\\Tx_Automate\\ApacheJmeter\\Test_Scripts\\UPCTest1.jmx" -l "D:\\Tx_Automate\\ApacheJmeter\\Results\\TestResults1.jtl" -e -o "D:\\Tx_Automate\\ApacheJmeter\\Results\\DashboardReports"'
        script{
        if(pipelineResult.equals('FAILURE'))
          {currentBuild.result = 'FAILURE'}}
      }
    }
  }
}
