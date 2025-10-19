pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo "Code checked out from repository."
            }
        }
        stage('Install Webserver & Dependencies') {
            steps {
                // Install Apache2 and PHP on the EC2 instance
                sh """
                sudo apt update -y
                sudo apt install -y apache2 php libapache2-mod-php
                sudo systemctl start apache2
                sudo systemctl enable apache2
                """
                echo "Apache2 and PHP are installed."
            }
        }
        stage('Deploy Application') {
            steps {
                // Copy the index.php file to the Apache web root
                // NOTE: This assumes Jenkins user has sudo permissions configured or you use SCP/SSH for deployment.
                sh 'sudo cp index.php /var/www/html/index.php'
                echo "Web page deployed to /var/www/html/."
            }
        }
        stage('Post-Deployment Verification') {
             steps {
                // Wait for the web server to fully load the page
                sleep 5
                // You would add Selenium IDE or manual test steps here.
                echo "Deployment verification complete. Check http://YOUR_EC2_IP"
            }
        }
    }
}
