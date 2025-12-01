pipeline{

agent any

tools
{
     maven 'maven_3.9.7'
}
	
environment
{
   buildNumber = "${BUILDNUMBER}"
}
	
stages{

  stage('CheckOutCode')
	{
    steps()
	  {
    git branch: 'docker-cicd', url: 'https://github.com/jvvenkateshgh/maven-web-application.git'
	  }  
	}

stage('Build Project')
    {
      steps()
      {
        sh "mvn clean package"
      }
    }
stage("Build Docker Image")
        {
            steps()
            {
                sh 'docker build -t jvvenkateshdh/docker-cicd:${buildNumber} .'
            }
        }

	
  }
}
