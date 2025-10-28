pipeline {
    agent any
	
    environment {
        REMOTE_USER = 'admin'
        REMOTE_HOST = 'server1'      // change to your RHEL VM IP
        SSH_CRED_ID = 'rhel-ssh'      // Jenkins credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone your GitHub repo
                git branch: 'main', url: 'https://github.com/Drixinside/My-Website'
            }
        }

        stage('Build') {
            steps {
                echo "Simulating build..."
                sh 'chmod +x ./app.sh'
		sh './app.sh'
            }
        }

        stage('Deploy to RHEL VM') 
            steps {
                sshagent(['rhel-ssh']) {
		    sh 'scp -o StrictHostKeyChecking=no ./app.sh ${REMOTE_USER}@${REMOTE_HOST}:/tmp/app.sh' 
                    sh 'ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} "bash /tmp/app.sh" "echo Deployed on $(hostname)"'
                }
            }
        }
    }
}

