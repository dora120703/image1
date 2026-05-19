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
        stage('A1: Resource Check') {
            steps {
                echo "Evaluating active environment context variables..."
                echo "Target Resource Name resolved to: ${IMAGE_NAME}"
            }
        }
        stage('A2: Run Cleanup Script') {
            steps {
                catchError {
                    // FIX 1: Navigate directly inside your 'ci' submodule directory context
                    dir('ci') {
                        // FIX 2: Switched to native Windows 'bat' execution block
                        bat 'cleanup_images.bat'
                    }
                }
            }
        }
    }
}
