pipeline {
    agent any
    
    stages {
        stage('SCM') { 
            steps {
                git 'https://github.com/arifislam007/btl-phone-directory' 
            }
        }
		
        stage('Send Over SSH Docker Host') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: 'dockerhost', 
					transfers: [sshTransfer(cleanRemote: false, excludes: '', 
					execCommand: '''cd /root/btlphonebook;
					docker build -t btlpnone:v1 .;
					docker stop btlphone;
					docker rm btlphone;
					docker run -itd --name btlphone -p 80:80 btlpnone:v1''', 
					execTimeout: 120000, flatten: false, makeEmptyDirs: false, 
					noDefaultExcludes: false, patternSeparator: '[, ]+', 
					remoteDirectory: 'btlphonebook', remoteDirectorySDF: false, 
					sourceFiles: '**/*')], 
					usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
               
            }
            
        }
    }
}