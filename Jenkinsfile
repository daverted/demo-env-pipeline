pipeline {
  agent any
  stages {
    stage('OverOps') {
      steps {
        OverOpsQuery(
          deploymentName: 'v4.44.3',
          serviceId: 'S37777',
          regexFilter: '"type":\\"*(Timer|Logged Warning|Logged Error)',
          markUnstable: true,
          printTopIssues: 10,
          newEvents: true,
          resurfacedErrors: true,
          maxErrorVolume: 0,
          maxUniqueErrors: 0,
          criticalExceptionTypes: 'AmazonClientException,ResourceNotFoundException,NullPointerException,IndexOutOfBoundsException,InvalidCastException,AssertionError',
          activeTimespan: '7d',
          baselineTimespan: '14d',
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
  }
}