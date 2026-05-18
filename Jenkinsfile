def runPipeline() {
    // 1. Prompt for extra parameters ONLY when Pipeline A runs
    def extraParams = input(
        id: 'PipelineAInputs',
        message: 'Pipeline A Configurations',
        parameters: [
            string(name: 'IMAGE_NAME', defaultValue: 'my-compute-image', description: 'Name of the VM Image'),
            choice(name: 'REGION', choices: ['us-central1', 'us-east1', 'europe-west1'], description: 'Target Cloud Region')
        ]
    )

    // 2. Access the extra inputs using the variable mapping
    stage('A1: Verify Manifests') {
        echo "Targeting Region: ${extraParams.REGION}"
        echo "Image name set to: ${extraParams.IMAGE_NAME}"
    }
    
    stage('A2: Bake Compute Image') {
        echo "Building VM Golden Image (${extraParams.IMAGE_NAME}-vA-${BUILD_NUMBER})..."
    }
    
    stage('A3: Rollout MIG A') {
        echo "Updating Managed Instance Group in ${extraParams.REGION}..."
    }
}
return this
