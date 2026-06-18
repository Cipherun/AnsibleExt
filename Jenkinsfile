pipeline {
    agent any
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven3'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Cipherun/AnsibleExt.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        
        stage('Deploy') {
            steps {
                
                        sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
                
            }
        }
        post{
            success{
                echo 'Build success'
            }
            failure{
                echo 'Build failure'
            }
        }
    }
}
