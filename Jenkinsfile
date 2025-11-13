pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/priyangshu-chakraborty/IndexDemo.git'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                // Ensure index.html exists in the workspace, then deploy
                sh '''
                  set -e
                  echo "Workspace: ${WORKSPACE}"
                  if [ ! -f "${WORKSPACE}/index.html" ]; then
                    echo "ERROR: index.html not found in workspace: ${WORKSPACE}"
                    echo "Listing workspace:"
                    ls -la "${WORKSPACE}"
                    exit 1
                  fi

                  echo "Cleaning /var/www/html ..."
                  rm -rf /var/www/html/*

                  echo "Copying index.html to /var/www/html ..."
                  cp "${WORKSPACE}/index.html" /var/www/html/

                  echo "Files in /var/www/html after copy:"
                  ls -la /var/www/html
                '''

                // Restart Nginx (requires root). If you prefer not to use sudo here,
                // add the sudoers entry shown below so Jenkins can run this without a password.
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
