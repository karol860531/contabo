pipeline {
    agent any
	
	parameters {
		string(
                                defaultValue: 'https://minecraft.azureedge.net/bin-linux/bedrock-server-1.19.10.03.zip',
                                name: 'URL',
                                trim: true)
		choice(
								choices: ['20000','20002','20202','30000'],
                                name: 'PORT',
								description: 'wybierz port serwera'
                                )	}			
	
    stages {
        stage('download') {
            steps {
                script {             
                    sh "pwd"
                    sh "curl -k ${params.URL} --output bedrock.zip"
                    sh "ls"
                    }
                }
            }
		
        stage('kill session') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                script {             
                    sh 'sudo killall -u minecraft'
                    } }
                }
            }
			
		stage('backup config file') {
            steps {
                script {
                    sh "whoami"
                    sh 'sudo cp /home/minecraft/$PORT/server.properties /home/minecraft/$PORT/server.properties_jenkins'
                    sh "ls"
                    }
                }
            }	
		
		stage('copy zip to folder') {
            steps {
                script {
                    sh "whoami"
                    sh 'sudo cp bedrock.zip /home/minecraft/$PORT'
                    sh "ls"
                    }
                }
            }	
		
			stage('unzip') {
            steps {
                script {
                    sh "whoami"
                    sh 'sudo unzip -o /home/minecraft/$PORT/bedrock.zip; sudo rm -f /home/minecraft/$PORT/bedrock.zip'
                    sh "ls"
                    }
                }
            }	
            
           	stage('chown') {
            steps {
                script {
                    sh "whoami"
                    sh 'sudo chown -R minecraft:minecraft /home/minecraft/$PORT/'
                    sh "ls"
                    }
                }
            }	
            
            stage('restore config file') {
            steps {
                script {
                    sh 'sudo cp /home/minecraft/$PORT/server.properties_jenkins /home/minecraft/$PORT/server.properties'
                    }
                }
            }
            
            stage('create tmux session and start bedrock') {
            steps {
                script {
                    sh 'JENKINS_NODE_COOKIE=dontkillme sudo screen -t $PORT -d -m "./home/minecraft/$PORT/start.sh"'
                    }
                }
            }
        }

        
}
