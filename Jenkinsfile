pipeline {
         agent any
         stages {
                 stage('Build Javascript') {
                 steps {

                 }
                 }
                 stage('Push to Docker') {
                     docker.withRegistry('https://registry.hub.docker.com', 'docker-hug-creden$')
                          app.push("${env.build_number}")
                          app.push("latest")

                 }
                 }
                 stage('Sonarqube') {
                      environment {
                          scannerHome =  tool 'SonarQubeScanner'
                      }

                      steps {
                      withSonarQubeEnv('sonarqube') {
                      sh "${scannerHome}/bin/sonar-scanner"
                      }
                    }
                      timeout (time: 10, unit: 'MINUTES'){
                      waitForQualityGate abortPipeline: true
                 }
                 }
                 stage('Deploy to Kubernates') {

                 }
}

