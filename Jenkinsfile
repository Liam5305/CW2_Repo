pipeline {
         agent any
         stages {
                 stage('Build Javascript') {
                 steps {
                     
                 }
                 }
                 stage('Push to Docker') {
                     docker.withRegistry('https://registry.hub.docker.com', 'docker-hug-credentials') {
                          app.push("${env.build_number}")
                          app.push("latest")
                      
                 }
                 }
                 stage('Deploy to Kubernates') {
                 
                 }
                 }
              }
}
