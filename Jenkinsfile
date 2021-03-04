pipeline {
	agent any
	
	environment{
	GIT_TAG = "4.0.436.0-(1.20.9.1) "
	}
	
  	stages {
		stage('Clone ndk repo') {
			 steps {
				 script {
						withCredentials([sshUserPrivateKey(credentialsId: 'git-ndk', keyFileVariable: '', passphraseVariable: '', usernameVariable: '')]) 
						{
                    					sh '''
								set -x
								rm -rf *
								git clone git@github.com:BuddyTV/ndk
							'''
						}
				 }
			 }
		 }
		
		stage("download tagged code to workspace"){
				steps {
					sh '''
					cd ndk
					
					
					
					'''
					//git checkout ${GIT_TAG}
					//sudo rm -rf *
					//cd ndk_plus_bsp
					//tag.tar.gz ${GIT_TAG}.tar.gz
									//mv !(ndk) tag
					//rm -rf Tag_${GIT_TAG} Tag_${GIT_TAG}@tmp
					//checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: 'git@github.com:BuddyTV/ndk', credentialsId: 'git-ndk' ]], branches: [[name: '${GIT_TAG}']]]
//sudo rm -rf ndk
					//cd ..
					//tar -czvf ${GIT_TAG}.tar.gz ndk_plus_bsp
					//cd ndk_plus_bsp
					//mkdir file
					
					//cd ..
					//mv ${GIT_TAG}.tar.gz ndk_plus_bsp
				}
			
		}

		stage('Uploading ndk & bsp to artifactory') {
            	steps {
                	rtUpload (
                   	serverId: 'artifactory',
                   	spec:
                       	     """{
                           	"files": [
                              	 	{
                               		   "pattern": "${GIT_TAG}.tar.gz",
                               		   "target": "vizio-dallas-megha-test/ndk/${GIT_TAG}"           								  
                              		}
                           		 ]
                       		  }"""
              		)
			//sh 'rm -rf *.tar.gz'
           	}
		}
		
	}
}
