pipeline {
    // Targets your specific Linux worker node natively
    agent { label 'built-in' } 
    
    environment {
        ZONE = 'europe-west2-a'
        SUBNETWORK = 'projects/hsbc-6320774-vpchost-au-dev/regions/europe-west2/subnetworks/cinternal-vpc1-europe-west2'
        CMEK = 'projects/hsbc-6320774-kms-dev/locations/europe-west2/keyRings/computeEngine/cryptoKeys/computeEngine'
        // This relies on the job name to build the real image resource name
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
                    // Simulates executing the script out of the checked-out submodule
                    sh 'echo "Running: sh ci/cleanup_images.sh for target resource ${IMAGE_NAME}"'
                }
            }
        }
    }
}
