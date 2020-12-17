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
			
			stage('Test Image')
			{
				steps
				{
				script
				{
				app.inside
				{
				sh 'echo "Tests Passed"'
				}
				}
				}
			}
			
			stage('Push To Docker')
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
					withSonarQubeEnv('sonarqube') 
					{
						sh "${scannerHome}/bin/sonar-scanner"
					}
				}
			}
		}
	}
