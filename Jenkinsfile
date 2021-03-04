pipeline {
	agent any
	
	environment{
	ndk_tag='4.0.436.0-(1.20.9.1)'
	ndk_bsp_tag = 'cbbccnk'
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
								git clone --branch ${ndk_tag} git@github.com:BuddyTV/ndk.git
							'''
						}
				 }
			 }
		 }
		
		stage("pack the files") {
			steps{
				sh ''' 
				set -x
				tar -czvf ${ndk_tag}.tar.gz ndk
				'''
			}
							

		}
		

		stage('Uploading ndk & bsp artifactory') {
            		steps {
                		rtUpload (
                   		serverId: 'artifactory',
                   		spec:
                       	 	    """{
                           		"files": [
                              	 		{
                               		   	"pattern": "(*).tar.gz(*)",
                               		  	 "target": "vizio-dallas-megha-test/"           								  
                              			}
                           			]
                       		  }"""
              			)
			//sh 'rm -rf *.tar.gz'
           		}
		}
		
	}
}
