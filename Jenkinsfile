pipeline {
         agent any
         stages {
                 stage('Build Javascript') 
                 {
                   steps {
                     script {

                       }
                     }
                   }
                 }
                 
                 stage('Build Image') 
                 {
                      app = docker.build("liam5305/linux_tweet_app:${env.BUILD_NUMBER}")
                 }

                 stage('Test Image') 
                 {
                   {
                     sh 'echo "Tests passed"'
                   }
                 }

                 stage('Push to Docker') 
                 {
                     steps {
                     script {
                          docker.withRegistry('https://registry.hub.docker.com', 'docker-hug-creden$')
                          {
                              app.push("${env.build_number}")
                              app.push("latest")
                          }
                     }
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
                      
                      timeout (time: 10, unit: 'MINUTES'){
                      waitForQualityGate abortPipeline: true
                      }
                    }
                 }
