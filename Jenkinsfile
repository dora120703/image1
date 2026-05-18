pipeline {
    agent any
    
    stages {
        stage('A1: Check Ansible Files') {
            steps {
                echo "Scanning playbooks and inventory configurations for Image 1..."
            }
        }
        stage('A2: Build VM Compute Image') {
            steps {
                echo "Baking VM Compute Image 1 from template files..."
            }
        }
        stage('A3: Deploy to MIG A') {
            steps {
                echo "Triggering rolling update for Managed Instance Group A..."
            }
        }
    }
}
