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
                    bat 'ci/cleanup_images.bat'
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
                bat 'ci/create_image.bat'
            }
        }
    }
}
