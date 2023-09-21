node { 

	def mavenName = tool name: "maven3"

	// properties([ pipelineTriggers([pollSCM('H/5 * * * *')]) ])


	stage('1st. - Clone Code from SCM'){
	
		echo "Clonning the code from Remote Repo on GitHub"

		git branch: 'scripted', changelog: false, poll: false, 
		url: 'https://github.com/ladio1z/tomcat-webapp-war.git'
	}


	stage('2nd. - Build the Scourc Code'){

		echo "Building Artifacts from the Scource Code"

		sh "${mavenName}/bin/mvn clean package"
	}

/*
	stage('3rd. - Code Quality Test for SonarQube'){
	
		echo "Do Code Quality Scan Test"

		sh "${mavenName}/bin/mvn sonar:sonar"
	}

*/

	stage('4th. - Intergrating Build Artifacts to Artifactory,Nexus'){

		echo "Intergrate Build Artifacts to Nexus"

		sh "${mavenName}/bin/mvn deploy"
	}

	
	stage('5th. - Deploying Build Artifact to Tomcat Server A'){

		echo "Deploying the Build Artifacts to Tomcat Server"

		deploy adapters: [tomcat9(credentialsId: 'Tomcat_Admin', path: '', 
		url: 'http://192.168.43.212:8800/')], contextPath: null, 
		onFailure: false, war: 'target/*.war'
	}

        
	stage('6th. - Deploying Build Artifact to Tomcat Server B'){

                echo "Deploying the Build Artifacts to Tomcat Server"

                deploy adapters: [tomcat9(credentialsId: 'Tomcat_Admin', path: '',
                url: 'http://192.168.33.27:8810/')], contextPath: null,
                onFailure: false, war: 'target/*.war'
        }



	stage('6th. - Scripted Pipeline Completed'){

		echo "Completion of Scripted Pipeline"

		echo "Thank YOU"
	}

}
