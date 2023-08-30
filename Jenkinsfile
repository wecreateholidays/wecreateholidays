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