pipeline {
    // 1. Tell the root declarative pipeline not to allocate an automatic node
    agent none 
    
    environment {
        ZONE = 'europe-west2-a'
        IMAGE_NAME = "poc-app1-image-${BUILD_NUMBER}"
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        stage('Cleanup') {
            // FIX: Removed 'agent any' from here so it stays inside 'poc2'
            steps {
                catchError {
                    dir('ansible') {
                        bat 'cleanup_images.bat'
                    }
                }
            }
        }
        
        stage('Apply Ansible config') {
            // FIX: Removed 'agent any' from here
            steps {
                dir('ansible') {
                    bat 'echo Executing playbooks out of the synced submodule directory...'
                }
            }
        }
        
        stage('Create Image') {
            // FIX: Removed 'agent any' from here
            steps {
                dir('ansible') {
                    bat 'create_image.bat'
                }
            }
        }
    }
}
