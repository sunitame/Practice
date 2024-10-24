pipeline {
    agent any // Use any available agent

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/sunitame/Practice.git' // Update with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image and tag it
                    sh 'docker build -t my-image:latest .'
                }
            }
        }

        stage('Save Image to Folder') {
            steps {
                script {
                    // Save the Docker image as a tar file in a specified folder
                    sh 'docker save my-image:latest -o ./saved_images/my_image.tar'
                }
            }
        }

        stage('Commit and Push') {
            steps {
                script {
                    // Commit the saved image and push it to the repo
                    sh '''
                        git config --global user.email "sunitameti@12gmail.com"
                        git config --global user.name "sunitame"
                        git add saved_images/my_image.tar
                        git commit -m "Add Docker image tar file"
                        git push
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
