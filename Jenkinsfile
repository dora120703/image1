pipeline {
    // Force the child stages to run directly in the parent node's workspace
    agent none 
    
    stages {
        stage('A1: Verify Layout') {
            agent any // Inherits the existing node, but forces compliance
            steps {
                echo "Locating submodule structure..."
                // Changed from 'sh ls' to Windows native 'bat dir'
                bat 'dir ansible' 
            }
        }
        stage('A2: Run Submodule Playbook') {
            agent any
            steps {
                dir('ansible') {
                    // Changed from 'sh' to 'bat'
                    bat 'echo Executing playbook block on Windows agent...'
                }
            }
        }
    }
}
