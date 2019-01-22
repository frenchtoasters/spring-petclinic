#!groovy
#def DOCKER_HUB_USER="frenchtoasters"

pipeline 
{
  agent any
    stages 
    {
       stage('Maven Install') 
       {
          steps 
          {
          sh 'mvn clean install'
          }
       }
      stage('Docker Build') 
       {
         steps 
         {
          sh 'docker build -t registry.gitlab.com/frenchtoasters/automated-jenkins:spring .'
         }
       }
      stage('Docker Push') 
      {
        steps 
        {
         withCredentials([usernamePassword(credentialsId: 'gitlabAccount', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) 
          {
            sh "docker login registry.gitlab.com -u $env.USERNAME -p $env.PASSWORD"
            sh "docker push registry.gitlab.com/frenchtoasters/automated-jenkins:spring"
            echo "Image push complete"
          }
        }
      }
      stage('Docker run') 
       {
         steps 
         {
          sh 'docker run -p 8082:8080 registry.gitlab.com/frenchtoasters/automated-jenkins:spring'
         }
       }
      
   }
}
