pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/JAASWANTH07/sample_repo.git'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                // Remove old HTML files
                sh 'sudo rm -rf /var/www/html/*'

                // Copy the new index.html file
                sh 'sudo cp index.html /var/www/html/'

                // Restart Nginx
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
