pipeline {
    agent any

    parameters {
        choice(
            name: 'ENV',
            choices: ['beta', 'prod'],
            description: 'Release env on which to deploy'
        )
    }


    stages {
        stage('Checkout'){
            steps {
                echo 'checkout WecreateHolidays codebase from git.'
            }
        }

        stage('Build'){
            steps {
                echo 'Creating deployable build.'
                echo "params received: ENV: ${params.ENV}"
            }
        }

        stage('Deploy'){
            steps {
                withCredentials([string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')]) { //set SECRET with the credential content
                    sh 'export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}'
                    sh 'export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}'
                    echo "Deploying WecreateHolidays on AWS EC2 instance env: ${params.ENV}"
                    sh "ansible-playbook ./ansible-playbooks/we_create_holidays.yaml -i we_create_holidays.aws_ec2.yaml --extra-vars \"envType=${params.ENV}\""
                    
                }
    
            }
        }

        stage('Post Deploy checks'){
            steps {
                echo 'post deploy checks successful.'
            }
        }
    }
}