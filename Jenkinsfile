pipeline {
    agent any
    stages {
        stage('Ansible Configure') {
            steps {
                dir('ansible') {
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
