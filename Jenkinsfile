pipeline {
    agent any
    stages {
        stage('A1: Verify Layout') {
            steps {
                echo "Locating submodule structure..."
                sh 'ls -la ansible/' // Verifies the folder is populated
            }
        }
        stage('A2: Run Submodule Playbook') {
            steps {
                dir('ansible') {
                    // Executes the playbook directly out of the submodule folder context
                    sh 'ansible-playbook playbook.yml'
                }
            }
        }
    }
}
