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
	
stages
{

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
        sh 'mvn clean package'
    }
  }
  stage("Build Docker Image")
  {
    steps()
    {
        sh 'docker build -t jvvenkateshdh/docker-cicd:${buildNumber} .'
    }
  }
  stage('Push Docker Image to Dockerhub Registry')
  { 
	steps()
	{
	     withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')]) 
		 {
			 sh 'docker login -u jvvenkateshdh -p ${Docker_Hub_Password}'
         }
		 sh 'docker push jvvenkateshdh/docker-cicd:${buildNumber}'
	}

  }

  stage('Remove Docker Image Localy in Jenkins Server')
  {
	steps()
	{
		sh 'docker rmi jvvenkateshdh/docker-cicd:${buildNumber}'
	}

  }

  stage('Deploy Aplication To Docker Deployment Server')
  {
	  steps()
	  {
		  sshagent(['Deployment_SSH']) 
		  {
			  sh "ssh -o StrictHostKeyChecking=no ubuntu@3.236.252.76 docker rm -f mavenwebaplication || true"
			  sh "ssh -o StrictHostKeyChecking=no ubuntu@3.236.252.76 docker run -d --name -p 8080:8080 jvvenkateshdh/docker-cicd:${buildNumber}"
          
		  }
	  }
   
  }
  

	
}

}

	
