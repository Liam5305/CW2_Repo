pipeline
	{
		agent any
		stages
		{	
			stage('Build Image')
			{
				steps
				{
					script
					{
						app = docker.build("liam5305/linux_tweet_app:${env.BUILD_NUMBER}")
					}
				}
			}
			
			stage('Push to Docker')
			{
				steps 
				{
				script 
				{
					 docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials')
					{
					 app.push("${env.build_number}")
						app.push("latest")
					}
				}
				}
			}
			
			stage('SonarQube')
			{
				environment
				{
					scannerHome = tool 'SonarQubeScanner'
				}
				
				steps
				{
					withSonarQubeEnv('SonarQube')
					{
						sh "${scannerHome}bin/sonar-scanner"
					}
				}
			}
			
			stage('Deploy to Kubernetes')
			{
				steps
				{
					script
					{
						sh "ssh ubuntu@3.238.251.90 \
						   kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=liam5305:${env.BUILD_NUMBER}"
					}
				}
			}
		}
	}
