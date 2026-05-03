pipeline {

    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                credentialsId: 'github-ssh',
                url: 'git@github.com:augustinein20/f5-config-deploy.git'
            }
        }

        stage('Verify Ansible') {
            steps {
                sh 'ansible --version'
            }
        }

        stage('Run F5 Deployment') {
            steps {
                sh '''
                ansible-playbook playbooks/deploy_virtual.yml
                '''
            }
        }
    }
}