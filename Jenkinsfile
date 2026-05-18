pipeline {
    // Standard declaration allows it to take over the primary workspace folder
    agent any 
    
    stages {
        stage('A1: Verify Layout') {
            steps {
                echo "Locating submodule structure..."
                // Runs natively inside the clean workspace path where submodules are loaded
                bat 'dir ansible' 
            }
        }
        stage('A2: Run Submodule Playbook') {
            steps {
                dir('ansible') {
                    bat 'echo Executing playbook block on Windows agent...'
                }
            }
        }
    }
}
