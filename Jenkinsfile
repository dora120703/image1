pipeline {
    // 1. You can now use your specific production build agent worker nodes natively!
    agent { label 'built-in' } 
    
    environment {
        ZONE = 'europe-west2-a'
        IMAGE_NAME = "poc-app1-image-${BUILD_NUMBER}"
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        stage('Cleanup') {
            steps {
                catchError {
                    dir('ansible') {
                        bat 'cleanup_images.bat'
                    }
                }
            }
        }
        
        stage('Apply Ansible config') {
            steps {
                dir('ansible') {
                    bat 'echo Executing playbooks out of the synced submodule directory...'
                }
            }
        }
        
        stage('Create Image') {
            steps {
                dir('ansible') {
                    bat 'create_image.bat'
                }
            }
        }
    }
}
