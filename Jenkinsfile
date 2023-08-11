pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = '/var/lib/tomcat9/webapps' // Set this to the actual path of the Tomcat webapps directory
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Copy HTML to Tomcat') {
            steps {
                // Copy the HTML file to the Tomcat webapps directory
               sh "sudo cp index.html /var/lib/tomcat9/webapps/ROOT/"  // Assumes the Tomcat ROOT application
            }
        }
    }
}
