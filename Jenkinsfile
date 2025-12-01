pipeline{

agent any

tools
{
     maven 'maven_3.9.7'

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
	
  }
}
