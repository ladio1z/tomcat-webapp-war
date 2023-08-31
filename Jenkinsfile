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
				            url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war.git'
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
        	stage('4 - Needing Confirmation before'){
			steps{
				echo "Needing Confimation"
                                
                          	timeout(15) {
					input message: "Please approve deployment "
			        }           
			}
		}
	       */


	        	
		stage('5 - Deploying Artifact to Tomcat - A '){
                        steps{
                                echo "Deploy an artifact to Tomcat A"
                                
                                deploy adapters: [tomcat9(credentialsId: 'Tomcat_Admin', 
				                 path: '', url: 'http://192.168.43.212:8800/')], 
		                		 contextPath: null, onFailure: false, war: '**/*.war'
			 }
                  } 

                
		 stage('6 - Deploying Artifact to Tomcat - B '){
                        steps{
                                echo "Deploy an artifact to Tomcat B"
                                           
                                deploy adapters: [tomcat9(credentialsId: 'Tomcat_Admin',
                                                 path: '', url: 'http://192.168.43.21:8180/')],
                                                 contextPath: null, onFailure: false, war: '**/*.war'
                         }
                  }



                /*
                stage(' 7. - Trigging the Scripted Pipeline '){		
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

