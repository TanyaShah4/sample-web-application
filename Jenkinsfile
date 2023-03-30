pipeline{
    agent any
    stages{
        stage("Sonarqube analysis"){
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'sonartoken') {
    // some block
}
                      sh 'mvn sonar:sonar'
                  }

                   timeout(5) {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                }
            }
        }
    }
    post{
        always{
          cleanWs()
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
