pipeline
{
  agent any

  tools
  {
  maven "maven-3.9.9"
  }
  triggers
   {
  pollSCM('* * * * *')
   }

  stages{

     stage('checkout'){

       steps{
        git credentialsId: '04ad7599-ea2d-45d2-bbd3-6fb2fa550d34', url: 'https://github.com/suresh1235/maven-web-app-project-kk-funda.git'
        }

     }

     stage('COMPILE'){
         steps{

         sh "mvn clean compile"

         }
     }

    stage('BUILD'){
         steps{

         sh "mvn clean package"

         }
     }

    stage('SQ REPORT'){
         steps{

         sh "mvn clean sonar:sonar"

         }
     }
    stage('Deploy to Nexus'){
         steps{

         sh "mvn clean deploy"

         }
     }

        stage('Deploy App'){
        steps{
         echo "Deploying WAR file using curl..."

        sh """
            curl -u kkfunda:password \
            --upload-file /var/lib/jenkins/workspace/jio-Scripted-dev-PL/target/maven-web-application.war \
            "http://43.204.114.41:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
        }
     }

  } //stages ending
  
} //pipeline ending
