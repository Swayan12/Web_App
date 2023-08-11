pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your HTML files from version control (e.g., Git)
                // If you're deploying a simple HTML page, just copy the files to a directory
            }
        }

        stage('Build') {
            steps {
                // Build step, if needed (not required for simple HTML deployment)
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    def response = httpRequest(
                        acceptType: 'APPLICATION_JSON',
                        contentType: 'APPLICATION_JSON',
                        httpMode: 'POST',
                        requestBody: [status: 'redeploy'],
                        url: "${http://13.53.176.154:8090/}/undeploy?path=${CONTEXT_PATH}"
                    )

                    if (response.status == 200) {
                        echo "Undeploy successful"
                    } else {
                        echo "Undeploy failed: ${response.status}"
                        error "Failed to undeploy the app"
                    }

                    response = httpRequest(
                        acceptType: 'APPLICATION_JSON',
                        contentType: 'APPLICATION_JSON',
                        httpMode: 'PUT',
                        requestBody: [war: file(target/*.war)],
                        url: "${http://13.53.176.154:8090/}/deploy?path=${CONTEXT_PATH}&update=true"
                    )

                    if (response.status == 200) {
                        echo "Deployment successful"
                    } else {
                        echo "Deployment failed: ${response.status}"
                        error "Failed to deploy the app"
                    }
                }
            }
        }
    }
}
