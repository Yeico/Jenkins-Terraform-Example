pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    tools
    {
        'org.jenkinsci.plugins.docker.commons.tools.DockerTool' 'Docker'
        'Terraform' 'Terraform'
    }
    environment {
    DOCKER_CERT_PATH = credentials('tareaSergi')
    }
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }
    stage('tfsec') {
      steps {
        sh 'docker --version'
      }
    }
    stage('Approval for Terraform') {
            steps {
                input(message: 'Approval required before Terraform', ok: 'Proceed', submitterParameter: 'APPROVER')
            }
        }

        stage('terraform') {
            steps {
              sh 'terraform init'
              sh 'terraform apply -auto-approve -no-color'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
