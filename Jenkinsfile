pipeline {
    // Mimic your production worker node designation
    agent { label 'built-in' } // Change this to match your available Windows agent label if needed
    
    environment {
        ZONE = 'europe-west2-a'
        IMAGE_NAME = "poc-app1-image-${BUILD_NUMBER}"
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        // Runs out of the main repository structure
        stage('Cleanup') {
            steps {
                catchError {
                    // FIX: Wrapped in dir('ansible') to avoid forward slash compilation errors on Windows
                    dir('ansible') {
                        bat 'cleanup_images.bat'
                    }
                }
            }
        }
        
        // Simulates running an automated playbook from your nested submodules
        stage('Apply Ansible config') {
            steps {
                dir('ansible') {
                    bat 'echo Executing playbooks out of the synced submodule directory...'
                }
            }
        }
        
        stage('Create Image') {
            steps {
                // FIX: Navigates inside the checked-out folder natively before executing the batch script
                dir('ansible') {
                    bat 'create_image.bat'
                }
            }
        }
    }
}
