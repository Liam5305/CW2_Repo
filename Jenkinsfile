pipeline
	{
		agent any
		stages
		{	
			stage('Build Image')
			{
				app = docker.build("liam5305/linux_tweet_app:${env.BUILD_NUMBER}")
			}
			
			stage('Push to Docker')
			{
				steps 
				{
				script 
				{
					 docker.withRegistry('https://registry.hub.docker.com', 'docker-hug-creden$')
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
<<<<<<< HEAD
		}
	}
=======
			
>>>>>>> e4de17a7ad0b5ffc5d80c03b9b66960e254bc942
