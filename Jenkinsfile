pipeline {
    agent any
    stages {
        stage('Terraform Apply') {
            steps {
                dir('terraform') {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve'
                }
            }
        }
        stage('Ansible Configure') {
            steps {
                dir('ansible') {
                    sh 'ansible-playbook -i inventory.ini playbook.yml'
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                dir('app') {
                    sh 'docker build -t mywebapp .'
                    sh 'docker run -d -p 80:80 mywebapp'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}