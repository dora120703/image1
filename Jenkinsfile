pipeline {
    agent { label 'built-in' } 
    
    environment {
        ZONE = 'europe-west2-a'
        SUBNETWORK = 'projects/hsbc-6320774-vpchost-au-dev/regions/europe-west2/subnetworks/cinternal-vpc1-europe-west2'
        CMEK = 'projects/hsbc-6320774-kms-dev/locations/europe-west2/keyRings/computeEngine/cryptoKeys/computeEngine'
        IMAGE_NAME = "${JOB_BASE_NAME}-v1-${BUILD_NUMBER}"
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        stage('A1: Pipeline A Start') {
            steps {
                echo "Evaluating context for Pipeline A (No extra parameters needed)..."
                echo "Target Resource Name: ${IMAGE_NAME}"
            }
        }
        stage('A2: Run Cleanup Script') {
            steps {
                dir('ci') {
                    bat 'cleanup_images.bat'
                }
            }
        }
    }
}
