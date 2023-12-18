pipeline {
    agent any
    tools{
        ansible 'ansible'
    }
    stages {
        stage('cleanws') {
            steps {
                cleanWs()
            }
        }
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Djay-ui/Ansible_2048.git'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }    
        stage('ansible provision') {
          steps {
             // To suppress warnings when you execute the playbook    
             sh "pip install --upgrade requests==2.20.1"
             ansiblePlaybook playbook: 'ec2.yaml' 
            }
        }
    }
}
