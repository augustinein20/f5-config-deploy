pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
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
                ansible-playbook f5-config-deploy/as3/deploy_virtual.yml -i inventory/hosts
                '''
            }
        }
    }

    post {
        failure {
            echo "Deployment failed. Please check Jenkins logs and Ansible output."
        }
    }
}