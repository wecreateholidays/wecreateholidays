pipeline {
    agent any

    stages {
        stage('Checkout'){
            steps {
                echo 'checkout WecreateHolidays codebase from git.'
            }
        }

        stage('Build'){
            steps {
                echo 'Creating deployable build.'
            }
        }

        stage('Deploy'){
            steps {
                withCredentials([string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID')]) { //set SECRET with the credential content
                    echo "My AWS access key id is '${AWS_ACCESS_KEY_ID}'"
                }
                echo 'Deploying WecreateHolidays on Aws'
                sh './ansible-playbooks/we_create_holidays.yaml'    
            }
        }

        stage('Post Deploy checks'){
            steps {
                echo 'post deploy checks successful.'
            }
        }
    }
}