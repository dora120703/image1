pipeline {
    // 1. Force the root pipeline template to run without assigning a new directory
    agent none 
    
    stages {
        stage('A1: Verify Layout') {
            agent {
                node {
                    // 2. Reuse the parent workspace explicitly to avoid getting tossed into @2
                    label 'built-in' // Use 'master' if you are on an older Jenkins version
                    customWorkspace "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\poc1"
                }
            }
            steps {
                echo "Locating submodule structure..."
                // Now this runs directly inside the primary 'poc1' folder where submodules exist
                bat 'dir ansible' 
            }
        }
        
        stage('A2: Run Submodule Playbook') {
            agent {
                node {
                    label 'built-in'
                    customWorkspace "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\poc1"
                }
            }
            steps {
                dir('ansible') {
                    bat 'echo Executing playbook block on Windows agent...'
                }
            }
        }
    }
}
