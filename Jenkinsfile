pipeline {
    agent any

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
                sh './app.sh'
            }
        }

        stage('Deploy to RHEL VM') {
            steps {
                sshagent(['rhel-ssh']) {
                    sh 'ssh -o StrictHostKeyChecking=no admin@server1 "echo Deployed on $(hostname)"'
                }
            }
        }
    }
}

