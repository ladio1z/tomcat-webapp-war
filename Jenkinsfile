pipeline { 

	agent any

	tools{
		maven 'maven3'
	}

       /*
        triggers{
		pollSCM('* * * * *')
	}
       */

	stages{

        	stage('1 - Clone from SCM'){
			steps{
				echo "Cloning from SCM "
		                
                                git branch: 'declarative', changelog: false, poll: false,
				            url: 'https://github.com/ladio1z/tomcat-webapp-war.git'
			}
		}

        	stage('2 - Build Artifacts'){
			steps{
				echo " Building an Artifact"
				sh "mvn clean package"
			}
		}

		
		/*
        	stage('3 - Sonar'){
			steps{
				echo "Code Quality Test"
				sh "mvn sonar:sonar"
			}
		}
		*/
                

                stage('3 - Storing Artifact in Nexus'){
                        steps{
                                echo "Keep artifact in Artifactory - Nexus"
                                sh "mvn deploy"
                        }
                }

              
                /*

                stage(' 4. - Trigging the CD Declartive Pipeline '){		
	              steps{
		       		echo "Triggering Upstream Declarative Pipeline"	
		   
		                build 'scripted1' 
			}
		}
               

                stage('8. - Scripted Pipeline Done'){		
	             steps{
		           echo "Completion to Scripted Pipeline"	

                           }
		  }

		*/


	  }

}

