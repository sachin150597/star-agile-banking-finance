pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/sachin150597/star-agile-banking-finance/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Build Image and expose') {
            steps {
                sh 'docker build -t sachin-image .'
                sh 'docker run -itd -p 8090:8090 --name mycontainer sachin-image'
            }
        }
         stage('Provision Test Server') {
            steps {
                // Provision test server using Terraform
                sh 'terraform apply -auto-approve'
            }
        }

        stage('Configure Test Server') {
            steps {
                // Configure test server using Ansible
                sh 'ansible-playbook -i inventory/hosts playbook.yml'
            }
        }
    }    
}
