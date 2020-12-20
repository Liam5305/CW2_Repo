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
					 docker.withRegistry('https://registry.hub.docker.com', 'docker-hug-credentials')
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
		}
	}
