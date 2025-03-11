 pipeline {
    agent any  // Runs on Jenkins default agent

    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/cndmphau/jenkins-pipeline-s1.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }

    post {
        success {
            sh 'terraform destroy -auto-approve'  // Optional cleanup
        }
    }
}
