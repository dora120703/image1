pipeline {
    agent { label 'built-in' }
    
    environment {
        ZONE = 'europe-west2-a'
        IMAGE_NAME = "${JOB_BASE_NAME}"
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        stage('Cleanup') {
            steps {
                catchError {
                    sh 'ci/cleanup_images.sh'
                }
            }
        }
        stage('Create Stage3 Instance') {
            steps {
                sh 'ci/create_stage3_instance.sh'
            }
        }
        stage('Apply Ansible config') {
            steps {
                sh 'ci/apply_ansible_config.sh'
            }
        }
        stage('Create Image') {
            steps {
                sh 'ci/create_image.sh'
            }
        }
        stage('Assign instance family') {
            steps {
                sh 'ci/assign_instance_family.sh'
            }
        }
    }
}
