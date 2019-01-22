#!groovy

pipeline
{
  agent any
    stages
    {
       stage('Maven Install')
       {
          steps
          {
          sh './mvnw package'
          }
       }
      stage('Java thing')
       {
         steps
         {
          sh 'java -jar target/*.jar'
         }
       }

   }
}

