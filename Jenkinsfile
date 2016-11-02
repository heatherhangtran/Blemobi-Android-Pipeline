stage ('build deploy') { 
     node{
         dir ('src/github.com/heatherhangtran/Blemobi-Android-Pipeline'){
         	git branch: '${BUILD_BRANCH}', credentialsId: 'JenkinsHK', url: 'https://github.com/blemobi/Blemobi-Android-Pipeline.git'
         
     		sh 'chmod +x gradlew'
     		stage "test"
     		sh './gradlew clean test'

     		stage "build"
     		sh './gradlew build createPom'
 
     		sh """
     		if [[ ${release} == "true"  &&   -v releaseVersion ]]
     		then
     		export GITHUB_TOKEN=${TOKEN}
        		cd $WORKSPACE/src/github.com/blemobi/${JOB_NAME}
	    		github-release release \
                  		--user blemobi \
 	            	        --repo ${JOB_NAME} \
     	         		--tag ${releaseVersion} \
 		 	        --name "${JOB_NAME} ${releaseVersion}" \
    	       			--description "${JOB_NAME} ${releaseVersion}" 
        	fi 	 
        	"""
	 }
     }
 }


      
