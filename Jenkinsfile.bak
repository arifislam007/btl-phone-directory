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
				sshPublisher(publishers: [sshPublisherDesc(configName: 'dockerhost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /root/btlphonebookv2;
					docker image rm btlpnone:v2;
					docker build -t btlpnone:v2 .;
					docker stop btlphonev2;
					docker rm btlphonev2;
					docker run -itd --name btlphonev2 -p 82:80 btlpnone:v2;''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
               
            }
            
        }
    }
}