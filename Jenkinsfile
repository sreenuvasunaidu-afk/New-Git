pipeline {
    agent any
    stages {
        stage('Checkout Code') {
        steps {
          echo 'Pulling latest code from GitHub...'
          git branch: 'main', url: 'https://github.com/sreenuvasunaidu-afk/New-Git.git'
          }
    }
        stage('Ansible Configure') {
            steps {
                dir('Ansible') {
                    sh 'ansible-playbook -i inventory.ini playbook.yaml'
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
