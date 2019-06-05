pipeline {
  agent any
  // agent {
  //   dockerfile {
  //     filename 'Dockerfile'
  //     // args '--link collector:collector'
  //   }
  // }
  stages {
    // stage('Build') {
    //   steps {
    //     sh './mvnw package -DskipTests'
    //   }
    // }
    // stage('Test') {
    //   environment {
    //     TAKIPI_SERVER_NAME = 'Jenkins'
    //   }
    //   steps {
    //     sh 'env'
    //     sh './mvnw -DargLine="-Dtakipi.application.name=${JOB_NAME} -Dtakipi.deployment.name=v0.1.0-${BUILD_NUMBER}" test'
    //   }
    // }
    stage('OverOps') {
      steps {
        OverOpsQuery(
          applicationName: 'OverOps',
          deploymentName: 'v4.36.1',
          // applicationName: '${JOB_NAME}',
          // deploymentName: 'v0.1.0-${BUILD_NUMBER}',
          serviceId: 'S37777',
          // regexFilter: '"type":\\"*(Timer|Logged Warning)',
          markUnstable: true,
          printTopIssues: 10,
          newEvents: true,
          resurfacedErrors: true,
          maxErrorVolume: 0,
          maxUniqueErrors: 0,
          criticalExceptionTypes: 'NullPointerException,IndexOutOfBoundsException,InvalidCastException,AssertionError',
          activeTimespan: '12h',
          baselineTimespan: '7d',
          minVolumeThreshold: 20,
          minErrorRateThreshold: 0.1,
          regressionDelta: 0.5,
          criticalRegressionDelta: 1.0,
          applySeasonality: true,
          debug: false
        )
        echo "OverOps Reliability Report: ${BUILD_URL}OverOpsReport/"
      }
    }
    stage('Build Status') {
      steps {
        echo "Build Status: ${currentBuild.currentResult}"
        echo "OverOps Query Success? ${currentBuild.resultIsBetterOrEqualTo('SUCCESS')}"
        echo "OverOps Query Unstable? ${currentBuild.resultIsWorseOrEqualTo('UNSTABLE')}"
        script {
          if (currentBuild.resultIsBetterOrEqualTo('SUCCESS')) {
            echo "Passed OverOps Quality Report"
          }
          if (currentBuild.resultIsWorseOrEqualTo('UNSTABLE')) {
            echo "Failed OverOps Quality Check"
          }
        }
      }
    }
    // stage('Deploy') {
    //   steps {
    //     sh 'echo "TODO"'
    //   }
    // }
  }
}